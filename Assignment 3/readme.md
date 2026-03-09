import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
import matplotlib.patches as mpatches
from sklearn.linear_model import LogisticRegression
from sklearn.neighbors import NearestNeighbors

# =============================================================================
# PHASE 1 — Bootstrapping Non-Parametric Uncertainty
# =============================================================================

# Step 1.1 — Zero-Inflated Tip Distribution
np.random.seed(42)
zeros = np.zeros(100)
tips = np.random.exponential(scale=5.0, size=150)
driver_tips = np.concatenate([zeros, tips])

print("=== Step 1.1 ===")
print(f"Sample size: {len(driver_tips)}")
print(f"Observed Median: ${np.median(driver_tips):.2f}")

# Step 1.2 — Manual Bootstrap Engine
n_iterations = 10000
bootstrap_medians = []

for _ in range(n_iterations):
    resample = np.random.choice(driver_tips, size=len(driver_tips), replace=True)
    bootstrap_medians.append(np.median(resample))

bootstrap_medians = np.array(bootstrap_medians)

lower = np.percentile(bootstrap_medians, 2.5)
upper = np.percentile(bootstrap_medians, 97.5)

print("\n=== Step 1.2 ===")
print(f"95% Confidence Interval: [${lower:.2f}, ${upper:.2f}]")

# =============================================================================
# PHASE 2 — Falsification in Logistics A/B Testing
# =============================================================================

# Step 2.1 — Synthetic A/B Test Data
np.random.seed(42)
control   = np.random.normal(loc=35, scale=5, size=500)
treatment = np.random.lognormal(mean=3.4, sigma=0.4, size=500)

observed_diff = np.mean(control) - np.mean(treatment)

print("\n=== Step 2.1 ===")
print(f"Control   — Mean: {np.mean(control):.2f}, SD: {np.std(control):.2f}")
print(f"Treatment — Mean: {np.mean(treatment):.2f}, SD: {np.std(treatment):.2f}")
print(f"Observed Difference (Control - Treatment): {observed_diff:.2f}")

# Step 2.2 — Manual Permutation Test
combined = np.concatenate([control, treatment])

n_iterations = 5000
simulated_diffs = []

for _ in range(n_iterations):
    shuffled = np.random.permutation(combined)
    group_a  = shuffled[:500]
    group_b  = shuffled[500:]
    simulated_diffs.append(np.mean(group_a) - np.mean(group_b))

simulated_diffs = np.array(simulated_diffs)
p_value = np.mean(np.abs(simulated_diffs) >= np.abs(observed_diff))

print("\n=== Step 2.2 ===")
print(f"Observed Difference: {observed_diff:.2f}")
print(f"Empirical P-value:   {p_value:.4f}")

# =============================================================================
# PHASE 3 — Causal Control & Selection Bias Mitigation
# =============================================================================

# Step 3.1 — Naive SDO
df = pd.read_csv('swiftcart_loyalty.csv')

subs     = df[df['subscriber'] == 1]
non_subs = df[df['subscriber'] == 0]

mean_subs     = subs['post_spend'].mean()
mean_non_subs = non_subs['post_spend'].mean()
SDO = mean_subs - mean_non_subs

print("\n=== Step 3.1 ===")
print(f"Mean Post-Spend (Subscribers):     ${mean_subs:.2f}")
print(f"Mean Post-Spend (Non-Subscribers): ${mean_non_subs:.2f}")
print(f"Naive SDO: ${SDO:.2f}  ({(SDO / mean_non_subs) * 100:.1f}% difference)")

# Step 3.2 — Propensity Score Matching (PSM)
covariates = ['pre_spend', 'account_age', 'support_tickets']
X = df[covariates]
D = df['subscriber']

model = LogisticRegression()
model.fit(X, D)
df['propensity_score'] = model.predict_proba(X)[:, 1]

subs     = df[df['subscriber'] == 1]
non_subs = df[df['subscriber'] == 0]

nn = NearestNeighbors(n_neighbors=1)
nn.fit(non_subs[['propensity_score']])
indices = nn.kneighbors(subs[['propensity_score']])[1].flatten()
matched_control = non_subs.iloc[indices]

ATT = subs['post_spend'].mean() - matched_control['post_spend'].mean()

print("\n=== Step 3.2 ===")
print(f"Causal ATT (PSM): ${ATT:.2f}")

# =============================================================================
# PHASE 4 — Love Plot
# =============================================================================

df_unmatched = df.copy()
df_matched   = pd.concat([subs, matched_control])

def compute_smd(dataframe, covariates):
    smds = {}
    treated = dataframe[dataframe['subscriber'] == 1]
    control = dataframe[dataframe['subscriber'] == 0]
    for col in covariates:
        diff   = treated[col].mean() - control[col].mean()
        pooled = np.sqrt((treated[col].std()**2 + control[col].std()**2) / 2)
        smds[col] = abs(diff / pooled)
    return smds

smd_before  = compute_smd(df_unmatched, covariates)
smd_after   = compute_smd(df_matched,   covariates)
features    = list(smd_before.keys())
vals_before = [smd_before[f] for f in features]
vals_after  = [smd_after[f]  for f in features]

fig, ax = plt.subplots(figsize=(9, 5))
fig.patch.set_facecolor('#0f1117')
ax.set_facecolor('#0f1117')

ax.axvline(x=0.1, color='#ff6b6b', linestyle='--', linewidth=1.2)
ax.axvline(x=0.0, color='white',   linestyle='-',  linewidth=0.5, alpha=0.3)

y_pos = range(len(features))
for i, feat in enumerate(features):
    ax.plot([vals_before[i], vals_after[i]], [i, i], color='#444', linewidth=1.5, zorder=1)
    ax.scatter(vals_before[i], i, color='#e05c5c', s=100, zorder=2)
    ax.scatter(vals_after[i],  i, color='#4fc3f7', s=100, zorder=2)

ax.set_yticks(list(y_pos))
ax.set_yticklabels(features, color='white', fontsize=12)
ax.set_xlabel('Absolute Standardized Mean Difference (SMD)', color='white', fontsize=11)
ax.set_title('Love Plot — Covariate Balance Before vs After PSM',
             color='white', fontsize=14, fontweight='bold', pad=15)
ax.tick_params(colors='white')
for spine in ax.spines.values():
    spine.set_edgecolor('#333')

ax.legend(
    handles=[
        mpatches.Patch(color='#e05c5c', label='Before Matching'),
        mpatches.Patch(color='#4fc3f7', label='After Matching'),
        mpatches.Patch(color='#ff6b6b', label='SMD = 0.1 threshold'),
    ],
    facecolor='#1a1d27', labelcolor='white', fontsize=10, loc='lower right'
)

plt.tight_layout()
plt.show()
