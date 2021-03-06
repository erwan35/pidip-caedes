dnl Process this file with autoconf to produce a configure script.

AC_INIT
AC_CONFIG_HEADER(include/pidip_config.h)

PDP_PIDIP_VERSION="0.12.20"
PD_DIR=/home/usune/DEB/src/puredata-0.41.4/pd-0.41-4/
PDP_DIR=/usr/include/pdp
FFMPEG_SOURCE_DIR=/SOURCES/ffmpeg
MPEG4IP_SOURCE_DIR=/SOURCES/mpeg4ip
PDP_STREAMING_OBJECTS=
PDP_CAPTURE_OBJECT=
IMLIB_LIBS=
IMLIB_CFLAGS=
MAGIC_LIBS=
MAGIC_CFLAGS=
THEORA_LIBS=
enable_ffmpeg=no
enable_mpeg4ip=no

#AC_ARG_WITH(pdsources, [  --with-pd=PATH          pd source tree])
#if ! test -z "${with_pd}"
#then
#  pd_tree="`cd ${with_pd} 2>/dev/null && pwd`"
#  if test -z "${pd_tree}"
#  then
#   dnl  The given directory can't be found
#   AC_MSG_ERROR([pd sources not found in ${with_pd}])
#  else
#   PD_DIR=${pd_tree}
#  fi
#fi

#AC_ARG_WITH(pdpsources, [  --with-pdp=PATH         pdp source tree])
#if ! test -z "${with_pdp}"
#then
#  pdp_tree="`cd ${with_pdp} 2>/dev/null && pwd`"
#  if test -z "${pdp_tree}"
#  then
#   dnl  The given directory can't be found
#   AC_MSG_ERROR([pdp sources not found in ${with_pdp}])
#  else
#   PDP_DIR=${pdp_tree}
#  fi
#fi

AC_ARG_WITH(ffmpeg, [  --with-ffmpeg=PATH      ffmpeg source tree])
if ! test -z "${with_ffmpeg}"
then
  ffmpeg_tree="`cd ${with_ffmpeg} 2>/dev/null && pwd`"
  if test -z "${ffmpeg_tree}"
  then
   dnl  The given directory can't be found
   AC_MSG_ERROR([ffmpeg sources not found in ${with_ffmpeg}])
  else
   FFMPEG_SOURCE_DIR=${ffmpeg_tree}
   enable_ffmpeg=yes
  fi
fi

AC_ARG_WITH(mpeg4ip, [  --with-mpeg4ip=PATH     mpeg4ip source tree])
if ! test -z "${with_mpeg4ip}"
then
  mpeg4ip_tree="`cd ${with_mpeg4ip} 2>/dev/null && pwd`"
  if test -z "${mpeg4ip_tree}"
  then
   dnl  The given directory can't be found
   AC_MSG_RESULT(no)
   AC_MSG_ERROR([mpeg4ip sources not found in ${with_mpeg4ip}])
  else
   MPEG4IP_SOURCE_DIR=${mpeg4ip_tree}
   enable_mpeg4ip=yes
  fi
fi

PDP_PIDIP_LIBS="$PDP_PIDIP_LIBS -lbz2 -lz -ldl -logg -lvorbis -lvorbisenc"
PDP_PIDIP_INCLUDES="-I$PD_DIR/src -I. -I$PDP_DIR -I../include -I../charmaps"

make clean

AC_ISC_POSIX
AC_PROG_CC
AM_PROG_CC_STDC
AC_HEADER_STDC
AC_PROG_INSTALL
AC_PROG_MAKE_SET
AM_SANITY_CHECK

AM_MAINTAINER_MODE
AM_WITH_DMALLOC

AC_PATH_GENERIC(imlib2, 1.0.0, [
  AC_SUBST(IMLIB_LIBS)
  AC_SUBST(IMLIB_CFLAGS) ],
  AC_MSG_ERROR(Cannot find imlib2: Is imlib2-config in the path?) )

dnl the above doesn't work for some reason :/
IMLIB_LIBS=`imlib2-config --libs`
IMLIB_CFLAGS=`imlib2-config --cflags`
AC_SUBST(IMLIB_LIBS)
AC_SUBST(IMLIB_CFLAGS)

CAIRO_CFLAGS="-I/usr/include/cairo/ -I/usr/local/include/cairo/"
AC_SUBST(CAIRO_CFLAGS)

#AC_CHECK_LIB(Magick, XWindowByProperty, , AC_MSG_ERROR(screen captures requires ImageMagick library!!), -I/usr/X11R6/include -L/usr/X11R6/lib )
AC_CHECK_LIB(bz2, BZ2_bzBuffToBuffCompress, , AC_MSG_ERROR(streaming requires bz2 library!!))
AC_CHECK_LIB(z, deflate, , AC_MSG_ERROR(streaming requires compress library!!))
AC_CHECK_LIB(dl, dlopen, , AC_MSG_ERROR(streaming requires dynamic loader library!!))
AC_CHECK_LIB(ogg, ogg_stream_init, , AC_MSG_ERROR(streaming requires ogg library!!), -lm)
#AC_CHECK_LIB(xine, xine_init, , AC_MSG_ERROR(pdp_xine requires xine library!!), -lm)
AC_CHECK_LIB(vorbis, vorbis_analysis_init, , AC_MSG_ERROR(streaming requires vorbis library!!), -lm)
AC_CHECK_LIB(vorbisenc, vorbis_encode_setup_init, , AC_MSG_ERROR(streaming requires vorbis encoder library!!), -lm)
AC_CHECK_LIB(theora, theora_encode_init, , AC_MSG_ERROR(theora library needed! sorry...), -lm)
AC_CHECK_LIB(quicktime, lqt_decode_video, , AC_MSG_ERROR(libquicktime not found) )

qt_minor_version="`lqt-config --version | cut -f3 -d'.'`"
qt_major_version="`lqt-config --version | cut -f1 -d'.'`"
echo "qt version minor : ${qt_minor_version} major : ${qt_major_version}"
       
IMLIB_CFLAGS="$CFLAGS -DQUICKTIME_NEWER=1"

if test ${qt_minor_version} == "8";
then
  IMLIB_CFLAGS="$CFLAGS -DQUICKTIME_NEWER=1"
fi
if test ${qt_minor_version} == "9";
then
  IMLIB_CFLAGS="$CFLAGS -DQUICKTIME_NEWER=1"
fi
if test ${qt_minor_version} == "10";
then
  IMLIB_CFLAGS="$CFLAGS -DQUICKTIME_NEWER=1"
fi
if test ${qt_minor_version} == "11";
then
  IMLIB_CFLAGS="$CFLAGS -DQUICKTIME_NEWER=1"
fi
if test ${qt_minor_version} == "12";
then
  IMLIB_CFLAGS="$CFLAGS -DQUICKTIME_NEWER=1"
fi
if test ${qt_major_version} == "1";
then
  IMLIB_CFLAGS="$CFLAGS -DQUICKTIME_NEWER=1"
fi
if test -f /usr/lib/libtheora.a
then
   THEORA_LIBS="$THEORA_LIBS /usr/lib/libtheora.a"
fi
if test -f /usr/local/lib/libtheora.a
then
   THEORA_LIBS="$THEORA_LIBS /usr/local/lib/libtheora.a"
fi
if test -f /usr/lib/libogg.a
then
   THEORA_LIBS="$THEORA_LIBS /usr/lib/libogg.a"
fi
if test -f /usr/local/lib/libogg.a
then
   THEORA_LIBS="$THEORA_LIBS /usr/local/lib/libogg.a"
fi
if test -f /usr/lib/libvorbis.a
then
   THEORA_LIBS="$THEORA_LIBS /usr/lib/libvorbis.a"
fi
if test -f /usr/local/lib/libvorbis.a
then
   THEORA_LIBS="$THEORA_LIBS /usr/local/lib/libvorbis.a"
fi
if test -f /usr/lib/libvorbisenc.a
then
   THEORA_LIBS="$THEORA_LIBS /usr/lib/libvorbisenc.a"
fi
if test -f /usr/local/lib/libvorbisenc.a
then
   THEORA_LIBS="$THEORA_LIBS /usr/local/lib/libvorbisenc.a"
fi

AC_SUBST(PDP_PIDIP_VERSION)

MAGICK_LIBS="-L/usr/X11R6/lib `Magick-config --libs` `Magick-config --ldflags`"
MAGICK_CFLAGS="-I/usr/X11R6/include `Magick-config --cflags` "
AC_SUBST(MAGICK_LIBS)
AC_SUBST(MAGICK_CFLAGS)

THEORA_LIBS="-ltheora -logg -lvorbis -lvorbisenc"

AC_SUBST(THEORA_LIBS)

echo -n "looking for pd sources (required) ... "
if test -f /usr/include/m_pd.h
then
  AC_SUBST(PD_DIR)
  echo "ok." 
else
  echo "pd source tree not found... install it and use the --with-pd=<path> configuration option."
  exit -1
fi

#echo -n "looking for pdp sources (required) ... "
#if test -f $PDP_DIR/CHANGES.LOG
#then
#  AC_SUBST(PDP_DIR)
#  echo "ok." 
#else
#  echo "pdp source tree not found... install it and use the --with-pdp=<path> configuration option."
#  exit -1
#fi
AC_CHECK_HEADER(linux/videodev2.h,
                PDP_CAPTURE_OBJECT="$PDP_CAPTURE_OBJECT pdp_v4l2.o"
                AC_DEFINE(HAVE_V4L2, 1, build pdp_v4l2),
                echo "   linux/videodev2.h not found: not building pdp_v4l2")

AC_CHECK_HEADER(libdv/dv.h,
                PDP_CAPTURE_OBJECT="$PDP_CAPTURE_OBJECT pdp_ieee1394l.o"
                PDP_PIDIP_LIBS="-ldv $PDP_PIDIP_LIBS"
                AC_DEFINE(HAVE_LIBDV, 1, build pdp_ieee1394 for linux),
                echo "   libdv/dv.h not found: not building pdp_ieee1394")


if test $enable_ffmpeg == yes;
then
  echo -n "looking for ffmpeg sources (required) ... "
  if test -f $FFMPEG_SOURCE_DIR/libavformat/avformat.h
  then
    AC_SUBST(FFMPEG_SOURCE_DIR)
    PDP_STREAMING_OBJECTS="pdp_live~.o pdp_ffmpeg~.o"
    AC_DEFINE(HAVE_PIDIP_FFMPEG, 1, build pdp_live~/pdp_ffmpeg~)
    PDP_PIDIP_LIBS="$PDP_PIDIP_LIBS $FFMPEG_SOURCE_DIR/libavformat/libavformat.a $FFMPEG_SOURCE_DIR/libavcodec/libavcodec.a"
    PDP_PIDIP_INCLUDES="$PDP_PIDIP_INCLUDES  -I$FFMPEG_SOURCE_DIR/libavcodec -I$FFMPEG_SOURCE_DIR/libavformat"
    echo "ok." 
  else
    echo "ffmpeg source tree not found... install it and use the --with-ffmpeg=<path> configuration option."
    exit -1
  fi
fi

if test $enable_mpeg4ip == yes;
then
   echo -n "looking for mpeg4ip sources (required) ... "
   if test -f $MPEG4IP_SOURCE_DIR/server/mp4live/mp4live_common.h
   then
    AC_SUBST(MPEG4IP_SOURCE_DIR)
    PDP_STREAMING_OBJECTS="pdp_mp4config.o pdp_mp4videosource.o pdp_mp4audiosource.o pdp_mp4live~.o pdp_mp4player~.o pdp_mp4audiosync.o pdp_mp4videosync.o pdp_mp4playermedia.o pdp_mp4playersession.o"
    AC_DEFINE(HAVE_PIDIP_MPEG4IP, 1, build pdp_mp4live~/pdp_mp4player~)
    PDP_PIDIP_LIBS="$PDP_PIDIP_LIBS $MPEG4IP_SOURCE_DIR/player/src/our_bytestream_file.o $MPEG4IP_SOURCE_DIR/player/src/our_config_file.o $MPEG4IP_SOURCE_DIR/player/src/qtime_file.o $MPEG4IP_SOURCE_DIR/player/src/mp4_file.o $MPEG4IP_SOURCE_DIR/player/src/mpeg3_file.o $MPEG4IP_SOURCE_DIR/player/src/avi_file.o $MPEG4IP_SOURCE_DIR/player/src/ip_port.o $MPEG4IP_SOURCE_DIR/player/src/media_utils.o $MPEG4IP_SOURCE_DIR/player/src/mpeg2t_thread.o $MPEG4IP_SOURCE_DIR/player/src/mpeg2t_thread_nx.o $MPEG4IP_SOURCE_DIR/player/src/*bytestream.o $MPEG4IP_SOURCE_DIR/player/src/*plugin.o $MPEG4IP_SOURCE_DIR/player/src/player_sdp.o $MPEG4IP_SOURCE_DIR/player/src/player_util.o $MPEG4IP_SOURCE_DIR/player/src/audio.o $MPEG4IP_SOURCE_DIR/player/src/video.o $MPEG4IP_SOURCE_DIR/server/mp4live/video_util_mpeg4.o $MPEG4IP_SOURCE_DIR/server/mp4live/sdp_file.o $MPEG4IP_SOURCE_DIR/server/mp4live/util.o $MPEG4IP_SOURCE_DIR/server/mp4live/video_encoder.o $MPEG4IP_SOURCE_DIR/server/mp4live/video_xvid.o $MPEG4IP_SOURCE_DIR/server/mp4live/media_source.o $MPEG4IP_SOURCE_DIR/server/mp4live/video_util_rgb.o $MPEG4IP_SOURCE_DIR/server/mp4live/video_util_resize.o $MPEG4IP_SOURCE_DIR/server/mp4live/resample.o $MPEG4IP_SOURCE_DIR/server/mp4live/video_encoder_base.o $MPEG4IP_SOURCE_DIR/server/mp4live/audio_encoder.o $MPEG4IP_SOURCE_DIR/server/mp4live/audio_encoder_base.o $MPEG4IP_SOURCE_DIR/server/mp4live/audio_encoder_tables.o $MPEG4IP_SOURCE_DIR/server/mp4live/audio_lame.o $MPEG4IP_SOURCE_DIR/server/mp4live/audio_faac.o $MPEG4IP_SOURCE_DIR/server/mp4live/rtp_transmitter.o $MPEG4IP_SOURCE_DIR/server/mp4live/h261/.libs/*.a $MPEG4IP_SOURCE_DIR/lib/sdp/.libs/libsdp.so $MPEG4IP_SOURCE_DIR/player/lib/mp4util/.libs/libmp4util.so $MPEG4IP_SOURCE_DIR/player/lib/libhttp/.libs/libhttp.a $MPEG4IP_SOURCE_DIR/lib/config_file/.libs/libconfig_file.so $MPEG4IP_SOURCE_DIR/lib/msg_queue/.libs/libmsg_queue.so $MPEG4IP_SOURCE_DIR/lib/mp4av/.libs/libmp4av.so $MPEG4IP_SOURCE_DIR/lib/mp4/.libs/libmp4.so $MPEG4IP_SOURCE_DIR/lib/mp4v2/.libs/libmp4v2.so $MPEG4IP_SOURCE_DIR/lib/SDL/src/.libs/libSDL.so $MPEG4IP_SOURCE_DIR/lib/rtp/*.o $MPEG4IP_SOURCE_DIR/player/lib/rtsp/.libs/librtsp.a $MPEG4IP_SOURCE_DIR/common/video/libmpeg32/.libs/*.a $MPEG4IP_SOURCE_DIR/lib/avi/.libs/libavi.al $MPEG4IP_SOURCE_DIR/lib/mpeg2t/.libs/libmpeg2_transport.al $MPEG4IP_SOURCE_DIR/player/lib/audio/mp3util/.libs/libmp3utils.al -lm -L/usr/X11R6/lib -lX11 -lXext -lpthread $MPEG4IP_SOURCE_DIR/lib/SDL/src/main/libSDLmain.a -ldl -Wl,--rpath -Wl,/usr/local/lib -lfaac -lmpeg4ip_xvid"
    PDP_PIDIP_INCLUDES="$PDP_PIDIP_INCLUDES -I/usr/include/SDL -I/usr/local/include/SDL -I$MPEG4IP_SOURCE_DIR/server/mp4live -I$MPEG4IP_SOURCE_DIR/player/src -I$MPEG4IP_SOURCE_DIR/player/lib -I$MPEG4IP_SOURCE_DIR/lib/msg_queue -I$MPEG4IP_SOURCE_DIR/lib"
    MPEG4IP_CFLAGS="-D_REENTRANT -DNOCONTROLS -fexceptions -Wno-char-subscripts -Wno-unknown-pragmas -Wno-deprecated -DPLAYER_PLUGIN_DIR=\"/usr/local/lib/mp4player_plugin\" -g -O2 -DUSE_MMX -DMPEG4IP"
    AC_SUBST(MPEG4IP_CFLAGS)
    echo "ok." 
  else
    echo "mpeg4ip source tree not found... install it and use the --with-mpeg4ip=<path> configuration option."
    exit -1
  fi
fi

AC_SUBST(PDP_PIDIP_VERSION)
AC_SUBST(IMLIB_LIBS)
AC_SUBST(IMLIB_CFLAGS)
AC_SUBST(THEORA_LIBS)
AC_SUBST(PDP_CAPTURE_OBJECT)
AC_SUBST(PDP_STREAMING_OBJECTS)
AC_SUBST(PDP_PIDIP_LIBS)
AC_SUBST(PDP_PIDIP_INCLUDES)

AC_CONFIG_FILES([
Makefile
system/Makefile
modules/Makefile
])
AC_OUTPUT

echo "used configure options:"
echo "  --enable-ffmpeg=$enable_ffmpeg"
echo "  --enable-mpeg4ip=$enable_mpeg4ip"
