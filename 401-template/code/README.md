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

p3_fig, p3_ax = plt.subplots(figsize=(9, 6))
p3_ax.scatter(p3_gen_f, p3_emp_f, label="Fossil", marker="o", color="#A64B2A")
p3_ax.scatter(p3_gen_n, p3_emp_n, label="Non-fossil", marker="^", color="#2E6F40")

p3_s, p3_i = np.polyfit(p3_gen_all, p3_emp_all, 1)
p3_ax.plot(p3_x, p3_i + p3_s * p3_x, "--", color="gray", linewidth=2,
           label=f"Pooled trend (r = {f13_r_pooled:.2f})")
p3_sf, p3_if = np.polyfit(p3_gen_f, p3_emp_f, 1)
p3_ax.plot(p3_x, p3_if + p3_sf * p3_x, ":", color="#A64B2A", linewidth=2,
           label=f"Fossil trend (r = {f13_r_fossil:.2f})")
p3_sn, p3_in = np.polyfit(p3_gen_n, p3_emp_n, 1)
p3_ax.plot(p3_x, p3_in + p3_sn * p3_x, ":", color="#2E6F40", linewidth=2,
           label=f"Non-fossil trend (r = {f13_r_nonfossil:.2f})")

p3_ax.axhline(0, linestyle="--", linewidth=0.8)
p3_ax.axvline(0, linestyle="--", linewidth=0.8)
p3_ax.set_title("Year-over-Year Generation Change vs. Employment Change, 2016\u20132025, Figure 3")
p3_ax.set_xlabel("Change in Generation Share (percentage points)")
p3_ax.set_ylabel("Employment % Change (year-over-year)")
p3_ax.legend(fontsize=8)
p3_ax.grid(True, alpha=0.3)
p3_fig.tight_layout()
plt.show()

















