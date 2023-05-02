import xarray as xr
import matplotlib.pyplot as plt
import cartopy.crs as ccrs
import cartopy.feature as cfeature

# Read the NetCDF file using xarray
ds = xr.open_dataset('GRIDMET DATA')

# Set the time range for the analysis
start_date = '1990-12-01'
end_date = '2020-12-31'

# Slice the dataset to the desired time period
ds_subset = ds.sel(day=slice(start_date, end_date))

# Calculate the annual climatology
climatology = ds_subset['tmax'].groupby('day.year').mean(dim='day')

# Convert temperature from Kelvin to Celsius
climatology_celsius = climatology - 273.15


# Plot the annual climatology
projection = ccrs.PlateCarree()
fig, ax = plt.subplots(nrows=1, ncols=1, figsize=(10, 6), subplot_kw={'projection': projection})

ax.set_title('Gridmet Annual Maximum Temperature Climatology (1991-2020)')
ax.set_extent([ds.lon.min(), ds.lon.max(), ds.lat.min(), ds.lat.max()], crs=projection)
ax.add_feature(cfeature.COASTLINE, linewidth=0.5)
ax.add_feature(cfeature.BORDERS, linewidth=0.5)
ax.add_feature(cfeature.STATES, linewidth =0.5)
ax.add_feature(cfeature.OCEAN)
im = ax.pcolormesh(ds.lon, ds.lat, climatology_celsius.mean(dim='year'), cmap='coolwarm', transform=projection)
ax.annotate('Data Source: Gridmet', xy=(0.05, 0.08), xycoords='axes fraction', fontsize=8, bbox=dict(facecolor='white', edgecolor='black', alpha=0.7, boxstyle='round,pad=0.5'))

plt.colorbar(im, ax=ax, orientation='horizontal', label='Temperature (°C)', pad=0.03)

fig.subplots_adjust(wspace=0.1, hspace=0.3)
plt.savefig('annual_climatology_air_temperature_1979_2020.png', dpi=300, bbox_inches='tight')
plt.show()
