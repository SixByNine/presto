SUBDIRS=slalib


lib_LTLIBRARIES=libpresto.la

# I thought about installing the headers, but I don't think they're used outside of presto
#libpresto_la_includedir=$(includedir)/presto/
#libpresto_la_include_HEADERS=accel.h database.h gmrt.h mpiprepsubband_cmd.h prepfold_cmd.h rawtype.h search_bin_cmd.h spigot2filterbank_cmd.h\
#	accelsearch_cmd.h dftfold.h imio.h multibeam.h prepsubband_cmd.h rdascat.h search_rzw_cmd.h toas2dat_cmd.h\
#	bincand_cmd.h dftfold_cmd.h makedata.h multifiles.h presto.h readfile_cmd.h show_pfd_cmd.h vectors.h\
#	bpp.h downsample_cmd.h makeinf.h orbint.h profile_cmd.h realfft_cmd.h sigproc_fb.h wapp.h\
#	cdflib.h f77.h mask.h plot2d.h psrfits.h rednoise_cmd.h slalib.h wapp_key.h\
#	chkio.h fitsfile.h meminfo.h prepdata_cmd.h randlib.h rfifind.h slamac.h wapp_y.tab.h\
#	clk_tck.h fitshead.h misc_utils.h prepfold.h ransomfft.h rfifind_cmd.h spigot.h zapbirds_cmd.h


bin_PROGRAMS = makedata makeinf mjd2cal realfft quicklook\
	   search_bin search_rzw swap_endian prepdata\
	   check_parkes_raw bary shiftdata dftfold\
	   patchdata readfile toas2dat taperaw\
	   accelsearch prepsubband cal2mjd split_parkes_beams\
	   dat2sdat sdat2dat downsample rednoise un_sc_td bincand\
	   dump_spigot_zerolag spigot2filterbank\
	   spigotSband2filterbank GBT350filterbank\
	   psrorbit window plotbincand prepfold show_pfd\
	   rfifind zapbirds explorefft exploredat weight_psrfits\
	   profile makewisdom


PRESTOOBJS = amoeba.c atwood.c barycenter.c birdzap.c cand_output.c\
	     characteristics.c cldj.c chkio.c corr_prep.c corr_routines.c\
	     correlations.c database.c dcdflib.c dispersion.c\
	     fastffts.c fftcalls.c fminbr.c fold.c fresnl.c ioinf.c\
	     get_candidates.c iomak.c ipmpar.c maximize_r.c maximize_rz.c\
	     median.c minifft.c misc_utils.c clipping.c\
	     orbint.c output.c read_fft.c responses.c\
	     rzinterp.c rzwinterp.c select.c sorter.c swapendian.c\
	     transpose.c twopass.c twopass_real_fwd.c\
	     twopass_real_inv.c vectors.c multifiles.c mask.c\
	     fitsfile.c hget.c hput.c imio.c

INSTRUMENTOBJS = multibeam.c bpp.c gmrt.c spigot.c sigproc_fb.c\
		 wapp.c wapp_head_parse.c wapp_y.tab.c psrfits.c


PLOT2DOBJS = powerplot.c xyline.c


DEFS=@FFTDEF@ -DUSEMMAP
LDADD=-lm -lpresto @FFTW_LIBS@
INCLUDES=@GLIB_CFLAGS@ @FFTW_CFLAGS@ @CFITSIO_CFLAGS@ @PGPLOT_CFLAGS@ -I$(PRESTO)/include

# Rules for CLIG generated files
%_cmd.c : ../clig/%_cmd.cli
	cd ../clig ; $(CLIG) -o $*_cmd -d $<
	mv ../clig/$*_cmd.h ../include/
	mv ../clig/$*_cmd.c .
	cp ../clig/$*.1 ../docs/


wisdom: makewisdom
	./makewisdom
	cp fftw_wisdom.txt $(PRESTO)/lib


libpresto_la_SOURCES=$(PRESTOOBJS) $(INSTRUMENTOBJS)

accelsearch_SOURCES= accelsearch_cmd.c accel_utils.c accelsearch.c zapping.c
accelsearch_LDADD=$(LDADD) @GLIB_LIBS@

bincand_SOURCES= bincand_cmd.c bincand.c

dftfold_SOURCES= dftfold_cmd.c dftfold.c

shiftdata_SOURCES= shiftdata.c

patchdata_SOURCES= patchdata.c

dat2sdat_SOURCES= dat2sdat.c

sdat2dat_SOURCES= sdat2dat.c

check_parkes_raw_SOURCES= check_parkes_raw.c

downsample_SOURCES=downsample.c downsample_cmd.c

rfifind_SOURCES=rfifind_cmd.c rfifind.c rfi_utils.c rfifind_plot.c range_parse.c $(PLOT2DOBJS)
rfifind_LDADD=$(LDADD) @CFITSIO_LIBS@ @PGPLOT_LIBS@


prepdata_SOURCES=prepdata_cmd.c prepdata.c
prepdata_LDADD=$(LDADD) @CFITSIO_LIBS@

prepsubband_SOURCES=prepsubband_cmd.c prepsubband.c $(PLOT2DOBJS)
prepsubband_LDADD=$(LDADD) @CFITSIO_LIBS@ @PGPLOT_LIBS@

prepfold_SOURCES=prepfold_cmd.c prepfold.c prepfold_utils.c prepfold_plot.c least_squares.f polycos.c readpar.c $(PLOT2DOBJS)
prepfold_LDADD=$(LDADD) @CFITSIO_LIBS@ @PGPLOT_LIBS@

spigot2filterbank_SOURCES=spigot2filterbank_cmd.c spigot2filterbank.c sla.c  
spigot2filterbank_LDADD=$(LDADD) -lsla

GBT350filterbank_SOURCES=GBT350filterbank.c  

spigotSband2filterbank_SOURCES=spigotSband2filterbank.c  

show_pfd_SOURCES=show_pfd_cmd.c show_pfd.c prepfold_utils.c prepfold_plot.c least_squares.f range_parse.c $(PLOT2DOBJS)
show_pfd_LDADD=$(LDADD) @PGPLOT_LIBS@

makedata_SOURCES=com.c randlib.c makedata.c

makeinf_SOURCES=makeinf.c 

mjd2cal_SOURCES=djcl.c mjd2cal.c

cal2mjd_SOURCES= cal2mjd.c

plotbincand_SOURCES= plotbincand.c $(PLOT2DOBJS)
plotbincand_LDADD=$(LDADD) @PGPLOT_LIBS@

profile_SOURCES= profile_cmd.c profile.c $(PLOT2DOBJS)
profile_LDADD=$(LDADD) @PGPLOT_LIBS@

psrorbit_SOURCES= psrorbit.c $(PLOT2DOBJS)
psrorbit_LDADD=$(LDADD) @PGPLOT_LIBS@


readfile_SOURCES= readfile_cmd.c readfile.c
readfile_LDADD=$(LDADD) @CFITSIO_LIBS@


realfft_SOURCES= realfft_cmd.c realfft.c

rednoise_SOURCES= rednoise.c rednoise_cmd.c

search_bin_SOURCES= search_bin_cmd.c search_bin.c

search_rzw_SOURCES= search_rzw_cmd.c search_rzw.c

taperaw_SOURCES= taperaw.c

toas2dat_SOURCES= toas2dat_cmd.c toas2dat.c


window_SOURCES= window.c $(PLOT2DOBJS)
window_LDADD=$(LDADD) @PGPLOT_LIBS@

zapbirds_SOURCES= zapbirds_cmd.c zapbirds.c zapping.c $(PLOT2DOBJS)
zapbirds_LDADD=$(LDADD) @PGPLOT_LIBS@ @GLIB_LIBS@
zapbirds_CFLAGS=@GLIB_CFLAGS@

explorefft_SOURCES= explorefft.c $(PLOT2DOBJS)
explorefft_LDADD=$(LDADD) @PGPLOT_LIBS@


exploredat_SOURCES= exploredat.c $(PLOT2DOBJS)
exploredat_LDADD=$(LDADD) @PGPLOT_LIBS@


weight_psrfits_SOURCES= weight_psrfits.c $(PLOT2DOBJS)
weight_psrfits_LDADD=$(LDADD) @CFITSIO_LIBS@ @PGPLOT_LIBS@


