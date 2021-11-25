## Create Cutout

```python
from astropy.coordinates import SkyCoord
from astropy.wcs import WCS

position = SkyCoord(hdu[0].header['CRVAL1']*u.deg,hdu[0].header['CRVAL2']*u.deg)
size = 200*u.pixel

wcs1 = WCS(hdu[0].header)

cutout = Cutout2D(hdu[0].data[0], position ,size, wcs = wcs1 )
```


Source: https://notebook.community/darioflute/CS4A/Lecture-astronomy

```python
from astropy.nddata import Cutout2D

size=400
cutout = Cutout2D(data, center, size, wcs=wcs)

print cutout.bbox_original

fig = plt.figure()
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8], 
                  projection=cutout.wcs)
#ax = plt.subplot(projection=wcs)
ax.set_xlabel('RA')
ax.set_ylabel('Dec')
ax.imshow(cutout.data, cmap='gist_heat',origin='lower')
ra = ax.coords[0]
ra.set_major_formatter('hh:mm:ss')
dec = ax.coords[1]
dec.set_major_formatter('dd:mm:ss');

# Making a Primary HDU (required):
primaryhdu= fits.PrimaryHDU(arr1)# Makes a header
# or if you have a header that you’ve created:
primaryhdu= fits.PrimaryHDU(arr1, header=head1)
# If you have additional extensions:
secondhdu= fits.ImageHDU(arr2)
# Making a new HDU List:
hdulist1 = fits.HDUList([primaryhdu, secondhdu])
# Writing the file:
hdulist1.writeto(filename, clobber=True)

cheader = cutout.wcs.to_header()
primaryhdu = fits.PrimaryHDU(cutout.data, cheader)
hdulist = fits.HDUList([primaryhdu])
hdulist.writeto('horse.fits', overwrite=True)
```
