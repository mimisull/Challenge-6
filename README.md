# Challenge-6
The Directory for this respoitory is:
[Summary](https://github.com/mimisull/Challenge-6/blob/main/README.md)
[Code](https://github.com/mimisull/Challenge-6/blob/main/san_francisco_housing.ipynb)

**Proptech Consulting for SF realestate**

Specifically, I am building a tool to offer an instant, one-click service for people to buy properties and then rent them. My company wants to have a trial of this offering in the San Francisco real-estate market. If the service proves popular, they can then expand to other markets.

I accomplish this using data visualization skills, including aggregation, interactive visualizations, and geospatial analysis, to find properties in the San Francisco market that are viable investment opportunities.

*User Story*:
As a user, I need to determine what are good investment opportunities.

As a user, I need to be able to visualize which neighborhoods in SF may fit this and trends over the years.

As a user, I need to have accurate and easy to read charts/diagrams to simplify my decision making process.

*Acceptance Criteria*:
Given that I’m unable to determine where good investment oppotunities are in the SF real estate market by talking to brokers, this will allow me to visualize it based off hard data trends..


## Usage
The project works by retrieving accurate data using transaction history, gross rent, and price per square footage, and finding rends in the market.

Imported the necessary tools with this code:

'''sfo_data_df = pd.read_csv(
    Path("./Resources/sfo_neighborhoods_census_data.csv"),
    index_col="year",
    parse_dates=True,
    infer_datetime_format=True)
sfo_data_df = sfo_data_df.dropna()'''

grouped by year with this:

'''housing_units_by_year = sfo_data_df.groupby('year').mean()'''
'''prices_square_foot_by_year = sfo_data_df.groupby('year').mean()'''
'''prices_square_foot_by_year = sfo_data_df[['sale_price_sqr_foot', 'gross_rent']].groupby('year').mean()'''
'''prices_by_year_by_neighborhood = sfo_data_df.groupby(['neighborhood', 'year']).mean()'''

visualized with this:

'''housing_units_by_year.hvplot.bar(ylim=(350000,385000), y='housing_units', x='year', figsize=(10,10), title='Housing Units in SF')'''
'''housing_units_by_year.hvplot(y="housing_units", x="year", title='Housing Units in SF')'''
'''prices_square_foot_by_year.hvplot(xlabel='year', ylabel='averages by dollar amount', title='Sales Prices per SQFT and Gross Rent')'''
'''prices_by_year_by_neighborhood.hvplot(x="year", groupby="neighborhood", title='Sales Prices per SQFT and Gross Rent')'''

Filtered with this:

'''prices_by_year_by_neighborhood = prices_by_year_by_neighborhood[['sale_price_sqr_foot', 'gross_rent']]'''

Loaded coordinates data with this:

'''neighborhood_locations_df = pd.read_csv(
    Path("./Resources/neighborhoods_coordinates.csv"),
    index_col="Neighborhood",
    parse_dates=True,
    infer_datetime_format=True)'''

Grouped by neighborhood:

'''all_neighborhood_info_df = sfo_data_df.groupby("neighborhood").mean()'''
'''ll_neighborhoods_df = pd.concat(
    [neighborhood_locations_df, all_neighborhood_info_df], 
    axis="columns",
    sort=False
)
'''

Geo plotted with this:

'''all_neighborhoods_df.hvplot.points(
    'Lon',
    'Lat',
    geo=True,
    color='gross_rent',
    tiles='OSM',
    size='sales_price_sqr_foot',
    frame_width=700,
    frame_height=500,
    title='Neighborhoods Pricing in SF')'''

## Contributors
Michael Sullivan

Cal Berkeley Fintech 

Kevin Lee
