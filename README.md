# Filtrer le dataset pour les équipes ayant gagné des médailles
medal_winners = df[df['Medal'].notna()]

# Séparer les datasets pour chaque type de médaille
gold_medals = medal_winners[medal_winners['Medal'] == 'Gold']
silver_medals = medal_winners[medal_winners['Medal'] == 'Silver']
bronze_medals = medal_winners[medal_winners['Medal'] == 'Bronze']

# Grouper par Année et Équipe, et agréger le nombre de joueurs NBA pour chaque type de médaille
gold_medals_grouped = gold_medals.groupby(['Year', 'Team']).agg({'NBA': 'sum'}).reset_index()
silver_medals_grouped = silver_medals.groupby(['Year', 'Team']).agg({'NBA': 'sum'}).reset_index()
bronze_medals_grouped = bronze_medals.groupby(['Year', 'Team']).agg({'NBA': 'sum'}).reset_index()

# Ajouter une colonne pour le type de médaille
gold_medals_grouped['Medal'] = 'Gold'
silver_medals_grouped['Medal'] = 'Silver'
bronze_medals_grouped['Medal'] = 'Bronze'

# Combiner les trois dataframes
combined_medals = pd.concat([gold_medals_grouped, silver_medals_grouped, bronze_medals_grouped])

# Créer le graphique
fig = px.bar(combined_medals, x='Year', y='NBA', color='Medal', 
             color_discrete_map={'Gold': '#FFD700', 'Silver': '#C0C0C0', 'Bronze': '#CD7F32'},
             title='Number of NBA Players on Medal-Winning Teams Over the Years')

# Personnaliser les info-bulles pour afficher les noms des équipes uniquement en survol
fig.update_traces(hovertemplate='<b>Team: %{text}</b><br>Year: %{x}<br>NBA Players: %{y}<extra></extra>')

# Ajouter les noms des équipes pour les info-bulles
fig.for_each_trace(lambda trace: trace.update(text=combined_medals['Team']))

# Mettre à jour la mise en page pour une meilleure lisibilité
fig.update_layout(
    xaxis_title='Year',
    yaxis_title='Number of NBA Players',
    legend_title='Medal',
    barmode='stack'
)

fig.show()

######################
df['Medal_Won'] = df['Medal'].notna()

# Calculate average number of NBA players for teams that won medals
medal_winners_avg = df[df['Medal_Won']].groupby('Team')['NBA'].mean().reset_index(name='Average_NBA_Players')
medal_winners_avg['Category'] = 'Medal Winners'

# Calculate average number of NBA players for teams that did not win medals
non_medal_winners_avg = df[~df['Medal_Won']].groupby('Team')['NBA'].mean().reset_index(name='Average_NBA_Players')
non_medal_winners_avg['Category'] = 'Non-Medal Winners'

# Combine both dataframes
combined_avg = pd.concat([medal_winners_avg, non_medal_winners_avg])

combined_avg.head()

##########################
# Add a 'Medal_Won' column
df['Medal_Won'] = df['Medal'].notna()

# Calculate average number of NBA players for each type of medal
gold_avg = df[df['Medal'] == 'Gold'].groupby('Team')['NBA'].mean().reset_index(name='Average_NBA_Players')
gold_avg['Category'] = 'Gold Medal'

silver_avg = df[df['Medal'] == 'Silver'].groupby('Team')['NBA'].mean().reset_index(name='Average_NBA_Players')
silver_avg['Category'] = 'Silver Medal'

bronze_avg = df[df['Medal'] == 'Bronze'].groupby('Team')['NBA'].mean().reset_index(name='Average_NBA_Players')
bronze_avg['Category'] = 'Bronze Medal'

# Calculate average number of NBA players for teams that did not win medals
no_medal_avg = df[~df['Medal_Won']].groupby('Team')['NBA'].mean().reset_index(name='Average_NBA_Players')
no_medal_avg['Category'] = 'No Medal'

# Combine all dataframes
combined_avg = pd.concat([gold_avg, silver_avg, bronze_avg, no_medal_avg])

combined_avg.head()

import plotly.express as px

# Create the plot
fig = px.bar(combined_avg, x='Category', y='Average_NBA_Players', color='Category',
             title='Average Number of NBA Players in Teams by Medal Type',
             text='Team', barmode='group')

# Customize hover data to show team names
fig.update_traces(textposition='outside', hovertemplate='<b>%{text}</b><br>Category: %{x}<br>Average NBA Players: %{y}<extra></extra>')

# Update layout for better readability
fig.update_layout(
    xaxis_title='Category',
    yaxis_title='Average Number of NBA Players',
    showlegend=False
)

fig.show()
