import pandas as pd
import plotly.express as px

# Use the provided DataFrame
df = final_data

# Add abbreviations for teams
abbreviations = {
    'United States': 'USA',
    'Soviet Union': 'SU',
    'China': 'CHN',
    'Egypt': 'EGY',
    'Italy': 'ITA',
    'Lithuania': 'LTU',
    'Germany': 'GER',
    'Brazil': 'BRA',
    'Argentina': 'ARG',
    'Spain': 'ESP'
}
df['Team_Abbr'] = df['Team'].map(abbreviations).fillna(df['Team'])

# Filter the dataset for teams that have won medals
medal_winners = df[df['Medal'].notna()]

# Split the datasets for each type of medal
gold_medals = medal_winners[medal_winners['Medal'] == 'Gold']
silver_medals = medal_winners[medal_winners['Medal'] == 'Silver']
bronze_medals = medal_winners[medal_winners['Medal'] == 'Bronze']

# Group by Year and Team, and aggregate the number of NBA players for each medal type
gold_medals_grouped = gold_medals.groupby(['Year', 'Team_Abbr']).agg({'NBA': 'sum'}).reset_index()
silver_medals_grouped = silver_medals.groupby(['Year', 'Team_Abbr']).agg({'NBA': 'sum'}).reset_index()
bronze_medals_grouped = bronze_medals.groupby(['Year', 'Team_Abbr']).agg({'NBA': 'sum'}).reset_index()

# Add a column for the medal type
gold_medals_grouped['Medal'] = 'Gold'
silver_medals_grouped['Medal'] = 'Silver'
bronze_medals_grouped['Medal'] = 'Bronze'

# Combine the three dataframes
combined_medals = pd.concat([gold_medals_grouped, silver_medals_grouped, bronze_medals_grouped])

# Filter to include only specific Olympic years
years = list(range(1948, 2025, 4))
combined_medals = combined_medals[combined_medals['Year'].isin(years)]

# Create the chart
fig = px.bar(combined_medals, x='Year', y='NBA', color='Medal', text='Team_Abbr',
             color_discrete_map={'Gold': '#FFD700', 'Silver': '#C0C0C0', 'Bronze': '#CD7F32'},
             title='Number of NBA Players on Medal-Winning Teams Over the Years')

# Customize hover information to display team names
fig.update_traces(textposition='inside', hovertemplate='<b>%{text}</b><br>Year: %{x}<br>NBA Players: %{y}<extra></extra>')

# Mark the absence of the USA in 1980 with a clearer annotation
fig.add_annotation(
    x=1980,
    y=6,
    text="USA did not participate due to political issues",
    showarrow=True,
    arrowhead=1,
    ax=0,
    ay=-40,
    bgcolor="rgba(255, 255, 255, 0.8)",
    bordercolor="black"
)

# Update layout for better readability
