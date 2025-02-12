# Carbon Mapper - Version Log

Carbon Mapper is committed to continuously improving its scientific algorithms, applying updates to both future and historical data when necessary. This practice, known as “reprocessing,” is a widely used approach in scientific data management that ensures data remain accurate, consistent, and aligned with the latest scientific understanding, algorithms, and calibration standards. Reprocessing ensures consistency across data versions and sources by harmonizing datasets from different missions and instruments. This is crucial for creating seamless time series that support accurate analysis and monitoring of long-term trends.

All updates to Carbon Mapper data are assigned a version number for each product level, with a detailed change log summarizing modifications and documenting the state of the corresponding algorithms. Each version reflects rigorously vetted algorithm improvements to enhance accuracy and reduce observation uncertainty. Our [Algorithm Theoretical Basis Document (ATBD)](https://assets.carbonmapper.org/documents/L3_L4%20Algorithm%20Theoretical%20Basis%20Document_formatted_10-24-24.pdf) contains algorithm justification for our most recent algorithms and citations with detailed overviews of our product levels and algorithms associated with each product level. Additional information about each product level can be found in our [Product Guide]( https://carbonmapper.org/articles/product-guide).

We periodically reprocess historical data to ensure that past datasets benefit from the most recent, validated, and reliable algorithms. Previous versions of historical data remain accessible to users who may need them for specific applications or comparisons. Each historical reprocessing builds on the strengths of our existing algorithms, further enhancing data accuracy and refining precision to provide even more reliable emission estimates.

* The Summary table has an overview of published data versions.
* The Detailed Version Notes thoroughly explain how algorithms changed in a specified collection and what instruments and gases are impacted.
* The FAQ section answers questions about how to use this change log and how to identify what version of a product you are looking at.

# Summary Table
**NOTE** Version 2 is guaranteed to include the changes listed under version 2 products. Version 1 may include incremental changes between v1 and v2. 

| **Version**                                  |                                                                  **High Level Notes**                                                                   | **Date Available** | **Processing SW**         |
|:---------------------------------------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------:|:-------------------|:--------------------------|
| jpl                                          |                                                  Data processed by NASA JPL (Jet Propulsion Laboratory                                                  | Aug 2016           | No version data available |
| v0                                           |                                                                 Initial data algorithms                                                                 | March 2023         | No version data available |
| [v1 (j001<sup>1</sup>)](#version1)           |                                                    Heterogenous algorithm iterations across sensors                                                     | July 2023          | \> 0.4.0                  |
| [v2 (j002<sup>1</sup>)](#version2)           |                                                               Visualization products only                                                               | Jan 2024           | \> 0.21.0                 |
| [v3 (j3<sup>1</sup>)](#version3)             | Stable release to include more sensors/gases, retrievals incorporate more atmospheric information, updated masking and robust uncertainty calculations  | Feb 2025           | \> 3.0.0                  |

<sup>1</sup> versions that begin with j, were processed by NASA JPL using the same algorithms as the associated v<#> version.

# Detailed Version Notes
Refer to the ATBD for an in depth scientific justification of algorithms. The L2B ATBD includes details about filter types (MF/MFA/MFAL) and Unit Absorption Spectrum. The L3/L4 ATBD includes details about dynamic vs static retrievals, simple vs concentric circles IME, and maximum Fetch)

**NOTE**: **<span style="color:red"> **bolded text** </span>** indicates changes to algorithms in current version

# Version 3 <a name="version3"></a>

## Quantification Products
### Tanager (TAN) 
#### CH4
##### L2b (collection: l2b-ch4-mfa-v3)
* Wave length window
  * ****<span style="color:red"> (2100, 2430) </span>****
* Bad pixel saturation thresholds
  * 2092-2098nm range: Threshold of 3
  * ****<span style="color:red"> 2400-2500nm range: Threshold of 1 </span>****
* Unit Absorption Spectrum 
  * Solar Zenith Angle is queried
  * ****<span style="color:red"> Column Water Vapor is now queried </span>****
  * ****<span style="color:red"> Elevation is now queried </span>****
* Misc Changes
  * **<span style="color:red"> Bilinear resampling used to orthorectify retrieved concentrations (previously this was nearest neighbor) </span>**
##### L3a (collection: l3a-ch4-mfa-v3)
* Uses dynamic threshold masking 
  * **<span style="color:red"> Updated dynamic mask fit line </span>**
* Simple IME Method
  * Maximum Fetch is 2500m
  * **<span style="color:red"> Quantified plume lengths (reported as fetch) are consistent with IME concentration mask length </span>**
  * **<span style="color:red"> Include center pixel for IME and plume length quantification </span>**

##### L4a
* Wind products used
  * HRRR data archive for plumes within the HRRR coverage area 
  * ECMWF_IFS or ERA5 from OpenMeteo globally
* Emission Quantification Uncertainty
  * Uncertainty is propagated according to uncertainties in wind speed, IME, and plume length 
  * IME uncertainty includes retrieval, masking and length terms 
#### CO2
##### L2b (collection: l2b-co2-mfal-v3)
* Wave length window
  * **<span style="color:red"> (1960, 2430) </span>**
* Bad pixel saturation thresholds
  * 2092-2098nm range: Threshold of 3
  * **<span style="color:red"> 2400-2500nm range: Threshold of 1 </span>**
* Unit Absorption Spectrum 
  * Solar Zenith Angle is queried
  * **<span style="color:red"> Column Water Vapor is now queried </span>**
  * **<span style="color:red"> Elevation is now queried </span>**
##### L3a (collection: l3a-co2-mfal-v3)
* Uses dynamic threshold masking 
  * **<span style="color:red"> Updated dynamic mask fit line </span>**
* Concentric Circles IME Method
  * Maximum Fetch is 2500m
  * **<span style="color:red"> Include center pixel for IME and plume length quantification </span>**
##### L4a
* Wind products used
  * HRRR data archive for plumes within the HRRR coverage area 
  * ECMWF_IFS or ERA5 from OpenMeteo globally
* Emission Quantification Uncertainty
  * Uncertainty propagated according to uncertainties in wind speed and in the ratio of IME divided by plume length. IME/L is treated as a signal variable.
### EMIT 
#### CH4
##### L2b (collection: l2b-ch4-mfa-v3)
* Wave length window
  * (2100, 2480)
* Bad pixel saturation thresholds
  * 2092-2098nm range: Threshold of 2
  * **<span style="color:red"> 2400-2500nm range: Threshold of 1 </span>**
* Unit Absorption Spectrum 
  * Solar Zenith Angle is queried
  * **<span style="color:red"> Column Water Vapor is now queried </span>**
  * **<span style="color:red"> Elevation is now queried </span>**
* Misc Changes
  * **<span style="color:red"> Uses correct geotransform from EMIT NetCDF metadata to eliminate small gaps between scenes </span>**
  * **<span style="color:red"> Projected to UTM to ensure consistency across instruments </span>**
##### L3a (collection: l3a-ch4-mfa-v3)
* Uses dynamic threshold masking 
  * **<span style="color:red"> Updated dynamic mask fit line</span>**
* Simple IME Method
  * **<span style="color:red"> Maximum Fetch is 2500m</span>**
  * **<span style="color:red"> Quantified plume lengths (reported as fetch) are consistent with IME concentration mask length</span>**
  * **<span style="color:red"> Include center pixel for IME and plume length quantification</span>**
##### L4a
* Wind products used
  * HRRR data archive for plumes within the HRRR coverage area 
  * ECMWF_IFS or ERA5 from OpenMeteo globally
  * **<span style="color:red">  HRRR winds are spatially averaged to match the resolution of ECMWF_IFS allowing for cross comparisons of plume uncertainties regardless of detection location</span>**
* Emission Quantification Uncertainty
  * **<span style="color:red"> Uncertainty propagated according to uncertainties in wind speed, IME, and plume length </span>**
  * **<span style="color:red"> IME uncertainty includes retrieval, masking and length terms</span>**
#### CO2
##### L2b (collection: L2b-co2-mfal-v3)
**<span style="color:red"> This is a change from previously used mfa to mfal products </span>**

* Wave length windows
  * **<span style="color:red"> (1860, 2190)</span>**
* Bad pixel saturation thresholds
  * **<span style="color:red"> 2092-2098nm range: Threshold of 2</span>**
  * **<span style="color:red"> 2400-2500nm range: Threshold of 1</span>**
* Unit Absorption Spectrum 
  * Solar Zenith Angle is queried
  * **<span style="color:red"> Column Water Vapor is now queried</span>**
  * **<span style="color:red"> Elevation is now queried</span>**
* Misc Changes
  * **<span style="color:red"> Uses correct geotransform from EMIT NetCDF metadata to eliminate small gaps between scenes</span>**
  * **<span style="color:red"> Projected to UTM to ensure consistency across instruments</span>**
##### L3a (collection: l3a-co2-mfal-v3)
* Uses dynamic threshold masking 
  * **<span style="color:red"> Updated dynamic mask fit line</span>**
* Concentric Circles IME Method
  * **<span style="color:red"> Maximum Fetch is 2500m</span>**
  * **<span style="color:red"> Include center pixel for IME and plume length quantification</span>**
##### L4a
* Wind products used
  * HRRR data archive for plumes within the HRRR coverage area 
  * ECMWF_IFS or ERA5 from OpenMeteo globally
  * **<span style="color:red"> HRRR winds are spatially averaged to match the resolution of ECMWF_IFS allowing for cross comparisons of plume uncertainties regardless of detection location </span>**
* Emission Quantification Uncertainty
  * Uncertainty propagated according to uncertainties in wind speed and in the ratio of IME divided by plume length. IME/L is treated as a signal variable.

### AVIRIS-3 (AV3) 
#### CH4
##### L2b (collection: l2b-ch4-mfa-v3)
* Wave length window
  * (2100, 2480)
* Bad pixel saturation thresholds
  * 2092-2098nm range: Threshold of 2
  * 2400-2500nm range: Threshold of 1
* Unit Absorption Spectrum 
  * Solar Zenith Angle, Column Water Vapor, and Elevation are queried
##### L3a (collection: l3a-ch4-mfa-v3)
* Uses dynamic threshold masking 
* Simple IME Method
  * Maximum Fetch is 284m
##### L4a
* Wind products used
  * HRRR data archive for plumes within the HRRR coverage area 
  * ECMWF_IFS or ERA5 from OpenMeteo globally
* Emission Quantification Uncertainty
  * Uncertainty propagated according to uncertainties in wind speed, IME, and plume length 
  * IME uncertainty includes retrieval, masking and length terms
#### CO2
##### L2b (collection: l2b-co2-mfal-v3)
* Wave length windows
  * (1860, 2190)
* Bad pixel saturation thresholds
  * 2092-2098nm range: Threshold of 2
  * 2400-2500nm range: Threshold of 1
* Unit Absorption Spectrum 
  * Solar Zenith Angle, Column Water Vapor, and Elevation are queried
##### L3a (collection: l3a-co2-mfal-v3)
* Uses dynamic threshold masking 
* Concentric Circles IME Method
  * Maximum Fetch is 284m
##### L4a
* Wind products used
  * HRRR data archive for plumes within the HRRR coverage area 
  * ECMWF_IFS or ERA5 from OpenMeteo globally
* Emission Quantification Uncertainty
  * Uncertainty propagated according to uncertainties in wind speed and in the ratio of IME divided by plume length. IME/L is treated as a signal variable.
### Global Airborne Observatory (GAO) & AVIRIS-NextGeneration (ANG) 
#### CH4
##### L2b (collection: l2b-ch4-mf-v3)
* Wave length window
  * (2100, 2480)
* Bad pixel saturation thresholds
  * 2092-2098nm range: Threshold of 4
  * **<span style="color:red"> 2400-2500nm range: Threshold of 1 </span>**
* Misc Changes
  * **<span style="color:red"> Rotation has been removed and rasters are now oriented northward </span>**
##### L3a (collection: l3a-ime-ch2-mf-v3)
* Uses static ppm-m threshold
  * 1000ppm-m
* Concentric Circles IME Method
  * Max Fetch 284m
  * **<span style="color:red"> Include center pixel for IME and plume length quantification </span>**
##### L4a
* Wind products used
  * HRRR data archive for plumes within the HRRR coverage area 
  * ECMWF_IFS or ERA5 from OpenMeteo globally
  * **<span style="color:red"> HRRR winds are spatially averaged to match the resolution of ECMWF_IFS allowing for cross comparisons of plume uncertainties regardless of detection location </span>**
* Emission Quantification Uncertainty
  * Uncertainty propagated according to uncertainties in wind speed and in the ratio of IME divided by plume length. IME/L is treated as a signal variable.
#### CO2
##### L2b (collection: l2b-co2-mfal-v3)
**<span style="color:red"> This is a change from previously used mfa to mfal products </span>**

* Wave length windows
  * (1860, 2190)
* Bad pixel saturation thresholds
  * **<span style="color:red"> 2092-2098nm range: Threshold of 4 </span>**
  * **<span style="color:red"> 2400-2500nm range: Threshold of 1 </span>**
* Unit Absorption Spectrum 
  * Solar Zenith Angle is queried
  * **<span style="color:red"> Column Water Vapor is now queried </span>**
  * **<span style="color:red"> Elevation is now queried </span>**
* Misc Changes
  * **<span style="color:red"> Rotation has been removed and rasters are now oriented northward </span>**

##### L3a (collection: l3a-co2-mfal-v3)
* Uses dynamic threshold masking 
  * **<span style="color:red"> Changed dynamic mask fit line </span>**
* Concentric Circles IME Method
  * Maximum Fetch is 284m
  * **<span style="color:red"> Include center pixel for IME and plume length quantification </span>**
##### L4a
* Wind products used
  * HRRR data archive for plumes within the HRRR coverage area 
  * ECMWF_IFS or ERA5 from OpenMeteo globally
  * **<span style="color:red"> HRRR winds are spatially averaged to match the resolution of ECMWF_IFS allowing for cross comparisons of plume uncertainties regardless of detection location</span>**
* Emission Quantification Uncertainty
  * Uncertainty propagated according to uncertainties in wind speed and in the ratio of IME divided by plume length. IME/L is treated as a signal variable.
## Visualization Products
* No changes 

# Version 2 (Visualization Products Only) <a name="version2"></a>
##### L2b (collection: l2b-rgb-v2)
* Implemented adaptive histogram stretching of radiance-based RGB
* Rotation has been removed from airborne products, and rasters are now oriented northward
* Uses correct geotransform from EMIT NetCDF metadata to eliminate small gaps between scenes
* Projected to UTM to ensure consistency across instruments
##### L3a (collection: l3a-vis-ch4-mf-v2, l3a-vis-ch4-mf-v002)
* Increased minimum concentration for colormap
* Made concentrations use the same extent as plume visualization
* Replaced vector plume thresholding with Gaussian blur process
* Added median filtering to input CMF
* Removed extra nodata within the plume and reduced box buffer size
* Raises an exception if no plume is found during thresholding
* Raises an exception if CH4 plumes grow too large
* Estimated background and clip concentrations before thresholding
* Included more pixels near plume origin in cases where origin doesn’t touch enhanced pixels
* Added metadata to tags in plume GeoTIFF
* Updated default crop size for PNG images
* Fix PNG rotation bug
* Replace distance-based subsetting with pixel-based to allow for EMIT
#### Non-Quantification Supplemental Products:
##### L2b (collection: l2b-ch4-mfm-v2)
Only produced for airborne scenes

##### L2b (collections: l2b-ch4-mfma-v2, l2b-co2-mfa-v2, l2b-co2-mfma-v2)
No Change

# Version 1 <a name="version1"></a>
##### L3a (collections: l3a-ime-ch4-mfa-v1, l3a-ime-co2-mfal-v1)
Derived from CMFs processed with or without the above improvements or processed in the field using unspecified code.
Quantification Products

### EMIT
##### L3a (collection: l3a-ime-ch4-mfa-v1)
* The radii increase of each concentric circle IME calculation has been changed to a constant of 1 pixel. 
* Max fetch distances are strictly calculated instead of using the nearest convex hull point distance.
* The use of a set 150x150 pixel tile crop for small enhancements has been removed.
* The extra buffering has been removed to accurately report the maximum fetch used in the computation.
* The standard max fetch distance is now set to 2500m
* New EMIT IME uncertainty (2024-07-26)

# Change Log FAQ

<details>
<summary>Q1 How can I tell what version of data I am looking at? (Click to expand)</summary>
  From the portal:

* (add screen shots)

From the STAC API (https://api.carbonmapper.org/api/v1/stac):
* Find the version in the properties of each STAC item.  For example:

```
{
  "type": "Feature",
  ...
  "properties": {
    ...
    "version": "v2"
  }
}
```

From downloaded spreadsheets
* (add example)
</details>

<details>
<summary>Q2 How do I know if algorithmic changes from one version to another impact the data I am looking at? (Click to expand)</summary>
  Note the version number of your data and find the corresponding section in this Change Log.  Within this section, note changes described for data grouped by product level (eg, “L3”, “L4”), instrument (eg, “EMIT”, “Tanager”), gas, etc. to identify changes to your specific data.  If your data have no changes described for the given version, then they are not impacted.
</details>

<details>
<summary>Q3 What does the version mean?  Why would it change? (Click to expand)</summary>
  Carbon Mapper works continuously to improve its algorithms for detecting and quantifying greenhouse gas emissions.  When an improvement is made and we begin using it to generate new data published on our portal, we will change the version number in the data to indicate that and to distinguish it from data generated with previous algorithms.
</details>

<details>
<summary>Q4 How frequently are new versions published?  Will I know in advance? (Click to expand)</summary>
  In the interest of providing the best data we can, Carbon Mapper may begin publishing new versions of data at any time without prior notice.  When a new version is published, only new data will have the new version.  Prior (historical) data generated with a previous version will remain unchanged.
From time to time, however, Carbon Mapper will reprocess some or all historical data using the latest version of its algorithms.  Such reprocessing will be announced in advance in this Change Log and other public communications.
</details>

<details>
<summary>Q5 How do I use a specific/fixed version of the data? (Click to expand)</summary>
  Carbon Mapper’s data portal (https://data.carbonmapper.org) always displays the most recent versions of the data.
Carbon Mapper’s STAC API (https://api.carbonmapper.org/api/v1/stac) can be used to retrieve previously published versions of data identified by the version number in the STAC collection name.
</details>

<details>
<summary>Q6 Whom can I contact for more information about changes and versioning? (Click to expand)</summary>
  Email Carbon Mapper at data@carbonmapper.org.
</details>


