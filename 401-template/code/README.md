# Code Folder

This folder contains code files for your project.

FIGURE 1
f13_fig1, f13_ax1 = plt.subplots(figsize=(10, 6))

for f13_source in f13_share_df.columns:
    f13_ax1.plot(
        f13_years,
        f13_share_df[f13_source],
        marker="o",
        label=f13_source
    )

f13_ax1.set_title(
    "U.S. Electricity Generation Share by Source, 2015–2025"
)
f13_ax1.set_xlabel("Year")
f13_ax1.set_ylabel("Share of Total U.S. Electricity Generation (%)")
f13_ax1.set_xticks(f13_years)
f13_ax1.legend()
f13_ax1.grid(True, alpha=0.3)
f13_fig1.tight_layout()
plt.show()




FIGURE 2
fig, ax = plt.subplots(figsize=(9, 5))

ax.plot(
    employment_df["Year"],
    employment_df["Fossil_Employment"],
    marker="o",
    label="Fossil Fuel"
)

ax.plot(
    employment_df["Year"],
    employment_df["NonFossil_Employment"],
    marker="o",
    label="Non-Fossil Fuel"
)

ax.set_title("U.S. Electricity Generation Employment, 2015–2025")
ax.set_xlabel("Year")
ax.set_ylabel("Employment")
ax.legend()
ax.grid(True, alpha=0.3)

fig.tight_layout()
plt.show()



FIGURE 3
f13_fossil_share = f13_share_df["Coal"] + f13_share_df["Natural Gas"]
f13_nonfossil_share = f13_share_df["Nuclear"] + f13_share_df["Solar"] + f13_share_df["Wind"]

f13_gen_shares = pd.DataFrame({
    "Year": [int(y) for y in f13_years],
    "Fossil_Generation_Share": f13_fossil_share.values,
    "NonFossil_Generation_Share": f13_nonfossil_share.values,
})

f13_merged = f13_gen_shares.merge(
    employment_df[["Year", "Fossil_Employment", "NonFossil_Employment"]], on="Year"
).sort_values("Year")

f13_merged["Fossil_Gen_Change"] = f13_merged["Fossil_Generation_Share"].diff()
f13_merged["NonFossil_Gen_Change"] = f13_merged["NonFossil_Generation_Share"].diff()
f13_merged["Fossil_Emp_Change"] = f13_merged["Fossil_Employment"].pct_change() * 100
f13_merged["NonFossil_Emp_Change"] = f13_merged["NonFossil_Employment"].pct_change() * 100

f13_df = f13_merged[f13_merged["Year"].between(2016, 2025)].copy()

f13_r_fossil, f13_p_fossil = stats.pearsonr(f13_df["Fossil_Gen_Change"], f13_df["Fossil_Emp_Change"])
f13_r_nonfossil, f13_p_nonfossil = stats.pearsonr(f13_df["NonFossil_Gen_Change"], f13_df["NonFossil_Emp_Change"])
f13_pooled_gen = pd.concat([f13_df["Fossil_Gen_Change"], f13_df["NonFossil_Gen_Change"]])
f13_pooled_emp = pd.concat([f13_df["Fossil_Emp_Change"], f13_df["NonFossil_Emp_Change"]])
f13_r_pooled, f13_p_pooled = stats.pearsonr(f13_pooled_gen, f13_pooled_emp)

print(f"Fossil-only r={f13_r_fossil:.3f}, p={f13_p_fossil:.3f}")
print(f"Non-fossil-only r={f13_r_nonfossil:.3f}, p={f13_p_nonfossil:.3f}")
print(f"Pooled r={f13_r_pooled:.3f}, p={f13_p_pooled:.3f}")

f13_long = pd.DataFrame({
    "dGen": list(f13_df["Fossil_Gen_Change"]) + list(f13_df["NonFossil_Gen_Change"]),
    "dEmp": list(f13_df["Fossil_Emp_Change"]) + list(f13_df["NonFossil_Emp_Change"]),
    "NonFossil": [0]*len(f13_df) + [1]*len(f13_df)
})
f13_X = sm.add_constant(f13_long[["dGen", "NonFossil"]])
f13_model = sm.OLS(f13_long["dEmp"], f13_X).fit()
print(f13_model.summary())

f13_b0 = f13_model.params["const"]
f13_b1 = f13_model.params["dGen"]
f13_b2 = f13_model.params["NonFossil"]
f13_p1 = f13_model.pvalues["dGen"]

f13_fig3, f13_ax3 = plt.subplots(figsize=(9, 6))
f13_ax3.scatter(f13_df["Fossil_Gen_Change"], f13_df["Fossil_Emp_Change"], label="Fossil", marker="o", color="#A64B2A")
f13_ax3.scatter(f13_df["NonFossil_Gen_Change"], f13_df["NonFossil_Emp_Change"], label="Non-fossil", marker="^", color="#2E6F40")

f13_xline = np.linspace(f13_pooled_gen.min()-0.3, f13_pooled_gen.max()+0.3, 50)
f13_ax3.plot(f13_xline, f13_b0 + f13_b1*f13_xline, "-", color="#A64B2A", linewidth=2, label="Fossil fitted (fixed effects)")
f13_ax3.plot(f13_xline, (f13_b0+f13_b2) + f13_b1*f13_xline, "-", color="#2E6F40", linewidth=2, label="Non-fossil fitted (fixed effects)")

f13_ax3.axhline(0, linestyle="--", linewidth=0.8)
f13_ax3.axvline(0, linestyle="--", linewidth=0.8)
f13_ax3.set_title("Year-over-Year Generation Change vs. Employment Change, 2016\u20132025")
f13_ax3.set_xlabel("Change in Generation Share (percentage points)")
f13_ax3.set_ylabel("Employment % Change (year-over-year)")
f13_ax3.legend(fontsize=8)
f13_ax3.grid(True, alpha=0.3)
f13_ax3.text(0.98, 0.03,
    f"Pooled Pearson r = {f13_r_pooled:.2f}, p = {f13_p_pooled:.2f}\n"
    f"Fixed-effects \u03b21 (within-group slope) = {f13_b1:.2f}, p = {f13_p1:.2f}",
    transform=f13_ax3.transAxes, fontsize=8.5, ha="right", va="bottom",
    bbox=dict(boxstyle="round", facecolor="#f5f5f0", edgecolor="gray"))
f13_fig3.tight_layout()
plt.show()


























