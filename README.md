# Presentasi-Magang-1

# 1.1 Introduction To Obspy
The types of Waveforms data, Inventory data, data request clients, metadata, stream and trace object, basic structure of Obspy's internal representation



# 1.2 Pre-processing data seismogram (waveform)


# 1.3 FDSN-Mass Downloader
## Rectangular Selection

obspy.clients.fdsn package contains a client to acces web servers that implement the FDSN web service definitions. Here are the step for downloading the seismic data:

1. specify the geographical region from which to download data;
2. define a number of other restrictions (temporal, data quality,...);
3. launch the download;

The mass downloader module will acquire all waveforms and associated station information across all known FDSN web service implementations producing a clean data set ready for further use. It works by:

a. figuring out what stations each provider offers;
b. downloading MiniSEED and associated StationXML meta information in an efficient and data center friendly manner, and
c. dealing with all the nasty real-world data issues like missing or incomplete data, duplicate data across data centers, e.g.

Basic optional automatic quality control by assuring that the data has no-gaps/overlaps or is available for a certain percentage of the requested time span.

It can relaunch download to acquire missing pieces which might happen for example if a data center has been offline.

It can assure that there always is a corresponding StationXML file for the waveforms.

## Data Set Selection
serves the purpose to limit the data to be downloaded to data useful for the purpose at hand. It is handled by two objects: subclasses of the Domain object and the Restrictions class.

The domain module currently defines three different domain types used to limit the geographical extent of the queried data: RectangularDomain, CircularDomain, and GlobalDomain. Subclassing Domain enables the construction of arbitrarily complex domains. Instances of these classes will later be passed to the function sparking the downloading process. 
Additional restrictions like temporal bounds, SEED identifier wildcards, and other things are set with the help of the Restrictions class are here:

1. starttime (UTCDateTime) – The start time of the data to be downloaded.
2. endtime (UTCDateTime) – The end time of the data.
3. network (str) – The network code. Can contain wildcards.
4. station (str) – The station code. Can contain wildcards.
5. location (str) – The location code. Can contain wildcards.
6. channel (str) – The channel code. Can contain wildcards.
7. reject_channels_with_gaps (bool) – If True (default), MiniSEED files with gaps and/or overlaps will be rejected.
8. minimum_length (float) – The minimum length of the data as a fraction of the requested time frame. After a channel has been downloaded it will be checked that its total length is at least that fraction of the requested time span. Will be rejected otherwise. Must be between 0.0 and 1.0, defaults to 0.9.
9. minimum_interstation_distance_in_m (float) – The minimum inter-station distance. Data from any new station closer to any existing station will not be downloaded. Also used for duplicate station detection as sometimes stations have different names for different webservice providers. Defaults to 1000 m.

## Storage Options
After determining what to download, the helpers must know where to store the requested data.


# 1.4 Instrument Corecction
Setiap stasiun perekaman data seismik memiliki spesifikasi alat yang berbeda bahkan model alat yang sama bisa jadi memiliki respon instrumen yang berbeda, belum lagi adanya pergantian sensor pada suatu stasiun seismik yang rusak, hal ini akan sangat memengaruhi cara kerja instrumen dalam melakukan perekaman dan menghasilkan data sehingga respon instrumen perlu dihilangkan dari data rekaman seismik agar dapat diperoleh hasil representasi aktual dari getaran di bawah permukaan Bumi. Pengabaian untuk menghapus respon instrumen yang bergantung pada frekuensi dari sensor seismik menghasilkan kesalahan amplitudo, fase, dan timing erors yang signifikan yang akan memengaruhi studi yang dilakukan seperti studi tomography, waktu dan lokasi gempa, studi gelombang permukaan, dan ambient noise cross corelation (Wilson et al., 2013). Menerapkan koreksi instrumen memungkinkan analisis seismogram dalam satuan fisik misalnya perpindahan, kecepatan, percepatan patikel. Masalah yang rumit adalah dalam praktiknya istilah "Koreksi Instrumen" lebih dari sekadar seismometer, koreksi instrumen mengkompensasi sistem perekaman lengkap termasuk seismometer, telemetri, digitizer, dan filter anti-alias apa pun (Matthew M. Haney et al, 2012).

# 1.5 Spectral Whitening


# 1.6 Normalization


