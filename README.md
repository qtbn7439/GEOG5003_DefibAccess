# GEOG5003_DefibAccess
Spatial Data Science Project into relationship between Deprivation and Defibrillator Accessibility

# Project Context:

**Research Question: Is accessibility to defibrillators lower in more deprived areas in Salford?**

According to the British Heart Foundation (2021), over 40,000 out of hospital cardiac arrest occur annually, with 10% surviving and a defibrillator being used in less than 10% cases. Lack of defibrillation reduces chances of survival by up to 10% every minute, whereas defibrillation within 3-5 minutes can produce survival rates of 50-70% (Perkins et al., 2015).

This report uses open spatial data to investigate the accessibility of defibrillators (AED) to deprivation levels using the study area of Salford, Greater Manchester. Accessibility is interpreted as either within reachable distance (200m) or freely available regardless of day, time or restrictions.

The analysis was carried using a Jupyter notebook to document the investigation and data analysis. 

# Data References:

**AED Data**

*Description:*
This data set provides location, availability and access type data of all defibrillators with a Guardian registered on The Circuit. It does not have personal details of the Guardian.

The data has been provided in good faith by the registered Guardians, but may be inaccurate, incomplete or out of date. The file is updated on the first working day of every month. It is being shared here to support relevant organisations, such as Local Authorities or charities, in making decisions on where to place more defibrillators. It may also be used by academics or researchers in the field of out-of-hospital cardiac arrest and the community response.

*Format:* csv

*Source:*

     Defibrillator data. (no date). [online] British Heart Foundation. Available at: https://www.bhf.org.uk/defibdata [Accessed 23 July 2026].



**Postcode Centroid Point Coordinates**

*Description:*
ONSPD latest Postcode Centroids
This file contains the digital vector centroids for the National Statistics Postcode Directory in the UK as at May 2026.
The centroids are of every live and terminated postcode in the United Kingdom.
Contains both Ordnance Survey and ONS Intellectual Property Rights. 

*Format:* GeoJson

*Source:*

         Statistics.gov.uk. (2026). ONSPD Online latest Postcode Centroids. [online] Available at: https://geoportal.statistics.gov.uk/datasets/84787e80aca04bb388caad29f89946b0_0/explore?location=53.486210%2c-2.229295%2c10 [Accessed 23 July 2026].



**Lower layer Super Output Areas (December 2021) Boundaries EW BGC (V5) - polygons**

*Description:* 
Census Boundaries
This file contains the digital vector boundaries for Lower layer Super Output Areas in England and Wales, as at 21 March 2021.
The boundaries available are: (BGC) Generalised (20m) - clipped to the coastline (Mean High Water mark).
Contains both Ordnance Survey and ONS Intellectual Property Rights.

LSOAs are small areas designed to be of a similar population size, with an average of approximately 1,600 residents or 650 households. There are 33,755 LSOAs in England. They are a standard statistical geography and were produced by the Office for National Statistics for the reporting of small area statistics. 

*Format:* GeoJson

*Source:*

		   
      Lower layer Super Output Areas (December 2021) Boundaries EW BGC (V5). (2021). [online] Statistics.gov.uk. Available at:https://geoportal.statistics.gov.uk/datasets/68515293204e43ca8ab56fa13ae8a547_0/explore?location=52.837634%2C-2.489483%2C7 [Accessed 23 July 2026].


**Indices of Multiple Deprivation Data**

*Description:*
Index of Multiple Deprivation (IMD) Rank and Decile for each LSOA. 

Deprivation refers to people’s unmet needs, a lack of access to opportunities and resources which we might expect in our society.
Index of Multiple Deprivation (IMD) combines information from the seven domains to produce an overall relative measure of deprivation. The domains are combined using the following weights:
Income Deprivation: 22.5%
Employment Deprivation: 22.5%
Education, Skills and Training Deprivation: 13.5%
Health and Disability Deprivation: 13.5%
Crime Deprivation: 9.3%
Barriers to Housing and Services Deprivation: 9.3%
Living Environment Deprivation: 9.3%

The weights have been derived from consideration of the academic literature on poverty and deprivation, as well as consideration of the levels of robustness of the indicators. A fuller account is given in section 3 and Appendix G of the IoD2025 Technical Report.

*Lower-layer Super Output Area (LSOA)*

LSOAs are small areas designed to be of a similar population size, with an average of approximately 1,600 residents or 650 households. There are 33,755 LSOAs in England. They are a standard statistical geography and were produced by the Office for National Statistics for the reporting of small area statistics. 

*Decile*

A decile is calculated by ranking the 33,755 neighbourhoods in England from most deprived to least deprived and dividing them into 10 equal groups (i.e. each containing 3,375 or 3,376 neighbourhoods). These deciles range from the most deprived 10 per cent of neighbourhoods nationally to the least deprived 10 per cent of neighbourhoods nationally.

*Official government statistics*

The IoD and IMD are accredited official statistics from Ministry of Housing, Communities & Local Government (MHCLG). The IoD have been produced by MHCLG and its predecessors since 2000. The IoD 2025 is the most recent release.
Format: csv

Source: 

    Indices of Deprivation 2025 Data. (2025). [online] Communities.gov.uk. Available at: https://deprivation.communities.gov.uk/ [Accessed 23 July 2026].





# Data Dictionary:

	LSOA21CD	- Lower Super Output Area Code
    LSOA21NM	- Lower Super Output Area Name
    LAD24CD	 - Local Authority Code
    LAD24NM - Local Authority Name
    geometry	- Point, line or polygon geometry of spatial items
    PCD7	- Post code
    UNIQUE_IDENTIFIER - Defibrillator reference from database	
    ADDRESS_POST_CODE	- Post Code
    DEFIBRILLATORS_AVAILABILITY	- Whether a defirbrillator is available 24/7 or has varied access
    DEFIBRILLATORS_ACCESS_TYPE	- Whether a defibrillator's access is public or restricted
    LAT	- latitude
    LONG	- longitude
    BNG_E	- British National Grid Easting
    BNG_N	- British National Grid Northing
    Distance - Calculated distance from postcode centroid to nearest defibrillator
    IMDRank	- National level Deprivation ranking (1 = highest deprivation)
    IMDDecile	- National level Deprivation decile (1 = highest deprivation)
    Salford_IMDRank	- Standardised local level Deprivation ranking (1 = highest deprivation)
    Salford_IMDDecile	- Standardised local level Deprivation decile (1 = highest deprivation)
    index_right	- Result of join to determine if postcode centroid intersects with walking distance buffer
    covered - boolean value - True = within buffer, false = outside buffer
    count - sum of how many in and out of buffer dependent on chosen grouping (LSOA, Decile)
    decile_total_postcodes	- total number of postcodes within decile
    LSOA_total_postcodes	- Total number of postcodes within a LSOA
    percentage_covered - percentage of postcodes within a decile/LSOA which are within the 200m buffer
    Covered	- percentage of postcodes within a decile/LSOA which are within the 200m buffer
    Not Covered - percentage of postcodes within a decile/LSOA which are outside the 200m buffer
    Average_Distance	- Average distance from postcode centroid to defibrillator per LSOA
    Coverage_Check - Check field to ensure that covered and not coveraged sum to 100%    
	x_group - generalised group to create bivariate choropleth to denote accessbility (average distance or percentage_covered)
    y_group - generalised group to create bivariate choropleth to denote deprivation 
    xy_group - concated x_group and y_group to create four quadrants of bivariate matrix
		


# Requirements for reproducing Analysis

All the data required to replicate this analysis are stored within the Data file within this GitHub repository. 

If wanting to replicate the analysis for another area, LSOA and Postcode Centroid data for the subset area should be sourced from the sources above. If needing to subset these from a larger dataset, the code is provided with the notebook commented out. 

Up to date versions of the debirilator data can be downloaded. 

Python libraries and packages required to install are within the notebook. 

