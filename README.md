<h1>The Analysis</h1>
<h2>1. What are the 3 most demanded skills for the top 3 most populsr data roles in Germany?</h2>
<p>To find the most demanded skills for the top 3 most popular data roles in germany. I first filtered my dataset to get only job postings in germany and then i filtered out the job descriptions by the 3 most popular. I finally filtered out the top skills for each of these job titles based on the percentage likelihood of each skill appearing in the job posting for a given role.</p>

<h3>View my notebook with detailed steps here:</h3>


[Skill Demand](Skill_Demand.ipynb)


## Visualize Data

```python 

fig, ax = plt.subplots(3, 1, figsize=(15, 9))
# Creating normalizer for hue
norm = mcolor.Normalize(
    vmin=df_skills["skill_percent"].min(), vmax=df_skills["skill_percent"].max()
)
sns.set_theme(style="ticks")
for i, val in enumerate(top_3_roles):
    plot_data = df_skills[df_skills["job_title_short"] == val].head()
    sns.barplot(
        data=plot_data,
        x="skill_percent",
        y=plot_data["job_skills"].str.upper(),
        hue="skill_percent",
        hue_norm=norm,
        palette=cmap,
        ax=ax[i],
        legend=False,
    )
    for x, v in enumerate(plot_data["skill_percent"]):
        ax[i].text(v + 1, x, f"{v:.0f}%", va="center", fontsize=14)
    ax[i].set_title(val, fontsize=20)
    ax[i].set_xlabel("")
    ax[i].set_ylabel("")
    ax[i].set_xlim(0, 65)
    ax[i].xaxis.set_visible(False)
    ax[i].tick_params(axis="y", labelsize=14)
    if i == len(top_3_roles) - 1:
        ax[i].xaxis.set_visible(True)
        ticks = ax[i].get_xticks()
        ax[i].set_xticks(ticks)
        ax[i].set_xticklabels(
            (f"{value}%" for value in ax[i].get_xticks()), fontsize=14
        )
    sns.despine(ax=ax[i])
fig.suptitle(
    ("Top skills by likelihood to appear in top 3 data roles in Germany").upper(),
    fontsize=28,
    color="#210221",
)
fig.tight_layout()
plt.show()
```

## Results
 [Visualization of top skills for top data jobs in Germany](images\plot_skill_demand.png)