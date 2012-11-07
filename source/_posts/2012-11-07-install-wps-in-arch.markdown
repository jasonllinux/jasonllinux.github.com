---
layout: post
title: "Arch中安装WPS A6"
date: 2012-11-07 16:33
comments: true
categories: Linux
---
最近终于申请到了wps a6，立马安装


* PKGBUILD

``` bash
pkgname=wps-office
pkgver=8.1.0.3431
_pkgver=8.1.0.3431+wps+wpp~a6
pkgrel=1
pkgdesc="Kingsoft Office is an office productivity suite. This is an ALPHA package and provides only Presentation. Use it at your own risk."
arch=('i686' 'x86_64')
license=("Custom")
url="http://www.wps.cn/"
depends=()
#makedepdends=('deb2targz' 'tar')
source=("${pkgname}_${_pkgver}_i386.deb")
sha1sums=('73cb05ef791fcfc46d884ae77015d1ee22bf2fcf')
install=${pkgname}.install 

if [ "${CARCH}" = 'x86_64' ]; then
  depends=('lib32-glib2' 'lib32-libxrender' 'lib32-libxext' 'lib32-libsm' 'lib32-fontconfig' )
else	
  depends=('glib2' 'libxrender' 'libxext' 'libsm' 'fontconfig' 'libjpeg6')
fi

package()
{
    cd "${srcdir}"
    tar azxvf data.tar.gz -C "${pkgdir}"
}

```


*wps-office.install

``` bash
#!/bin/bash

ksv_xdg_dirs=${XDG_DATA_DIRS:-/usr/share}
ksv_xdg_dir=
ksv_def_icon_theme=icons/hicolor

ksv_wps_mimes=('application-wps-office.wps' 'wps-office-wps.png' 'application-wps-office.wpt' 'wps-office-wpt.png')
ksv_word_mimes=('application-wps-office.doc' 'wps-office-doc.png' 'application-wps-office.dot' 'wps-office-dot.png' 'application-vnd.ms-word' 'wps-office-doc.png' 'application-msword' 'wps-office-doc.png' 'application-msword-template' 'wps-office-dot.png')
ksv_et_mimes=('application-wps-office.et' 'wps-office-et.png' 'application-wps-office.ett' 'wps-office-ett.png')
ksv_excel_mimes=('application-wps-office.xls' 'wps-office-xls.png' 'application-wps-office.xlt' 'wps-office-xlt.png' 'application-vnd.ms-excel' 'wps-office-xls.png' 'application-msexcel' 'wps-office-xls.png')
ksv_wpp_mimes=('application-wps-office.dps' 'wps-office-dps.png' 'application-wps-office.dpt' 'wps-office-dpt.png')
ksv_ppt_mimes=('application-wps-office.ppt' 'wps-office-ppt.png' 'application-wps-office.pptx' 'wps-office-ppt.png' 'application-wps-office.pot' 'wps-office-pot.png' 'application-vnd.ms-powerpoint' 'wps-office-ppt.png' 'application-vnd.mspowerpoint' 'wps-office-ppt.png' 'application-powerpoint' 'wps-office-ppt.png')

function ks_install_icon()
{
	local context=$1
	shift
	local mode=$1
	shift

	local png=
	local mime=
	local nextIsPng=0
	for item in $@
	do
		if [ "" = "${item}" ] ; then
			continue
		fi
		if [ ${nextIsPng} -eq 1 ] ; then
			png=${item}
			for i in 48 32 22 16; do
				if [ -e "${ksv_xdg_dir}/${ksv_def_icon_theme}/${i}x${i}/${context}/${png}" ] ; then
					xdg-icon-resource install --noupdate --mode ${mode} --context ${context} --size ${i} "${ksv_xdg_dir}/${ksv_def_icon_theme}/${i}x${i}/${context}/${png}" ${mime}
				fi
			done
			nextIsPng=0
		else
			mime=${item}
			nextIsPng=1
		fi
	done
}

function ks_config_default_mime_open()
{
	local desktop=$1
	shift

	local png=
	local mime=
	local nextIsPng=0
	for item in $@
	do
		if [ "" = "${item}" ] ; then
			continue
		fi
		if [ ${nextIsPng} -eq 1 ] ; then
			png=${item}
			nextIsPng=0
		else
			mime=${item/application-/application/}
			nextIsPng=1
		fi
	done
}

function ks_init()
{
	set -e
	for i in `echo "${ksv_xdg_dirs}" | sed 's/:/ /g'`
	do
		if [ -w ${i}/${ksv_def_icon_theme} ] ; then
			ksv_xdg_dir="${i}"
		fi
	done
}

function ks_config_menu()
{
	if [ -f "${ksv_xdg_dir}/applications/wps-office-et.desktop" ] ; then
		xdg-mime install --novendor --mode system "${ksv_xdg_dir}/mime/packages/wps-office-et.xml"

		xdg-desktop-menu install --noupdate --novendor --mode system "${ksv_xdg_dir}/applications/wps-office-et.desktop"
		#xdg-desktop-menu install --noupdate --novendor --mode system "${ksv_xdg_dir}/desktop-directories/wps-office.directory" "${ksv_xdg_dir}/applications/wps-office-et.desktop"
		xdg-desktop-menu forceupdate --mode system

		ks_install_icon "mimetypes" "system" "${ksv_et_mimes[*]}" "${ksv_excel_mimes[*]}"
		xdg-icon-resource forceupdate --mode system

		ks_config_default_mime_open "${ksv_xdg_dir}/applications/wps-office-et.desktop" "${ksv_et_mimes[*]}" "${ksv_excel_mimes[*]}"
	fi

	if [ -f "${ksv_xdg_dir}/applications/wps-office-wpp.desktop" ] ; then
		xdg-mime install --novendor --mode system "${ksv_xdg_dir}/mime/packages/wps-office-wpp.xml"

		xdg-desktop-menu install --noupdate --novendor --mode system "${ksv_xdg_dir}/applications/wps-office-wpp.desktop"
		#xdg-desktop-menu install --noupdate --novendor --mode system "${ksv_xdg_dir}/desktop-directories/wps-office.directory" "${ksv_xdg_dir}/applications/wps-office-wpp.desktop"
		xdg-desktop-menu forceupdate --mode system

		ks_install_icon "mimetypes" "system" "${ksv_wpp_mimes[*]}" "${ksv_ppt_mimes[*]}"
		xdg-icon-resource forceupdate --mode system

		ks_config_default_mime_open "${ksv_xdg_dir}/applications/wps-office-wpp.desktop" "${ksv_wpp_mimes[*]}" "${ksv_ppt_mimes[*]}"
	fi

	if [ -f "${ksv_xdg_dir}/applications/wps-office-wps.desktop" ] ; then
		xdg-mime install --novendor --mode system "${ksv_xdg_dir}/mime/packages/wps-office-wps.xml"

		xdg-desktop-menu install --noupdate --novendor --mode system "${ksv_xdg_dir}/applications/wps-office-wps.desktop"
		#xdg-desktop-menu install --noupdate --novendor --mode system "${ksv_xdg_dir}/desktop-directories/wps-office.directory" "${ksv_xdg_dir}/applications/wps-office-wps.desktop"
		xdg-desktop-menu forceupdate --mode system

		ks_install_icon "mimetypes" "system" "${ksv_wps_mimes[*]}" "${ksv_word_mimes[*]}"
		xdg-icon-resource forceupdate --mode system

		ks_config_default_mime_open "${ksv_xdg_dir}/applications/wps-office-wps.desktop" "${ksv_wps_mimes[*]}" "${ksv_word_mimes[*]}"
	fi
}

function ks_config_fonts()
{
	if [ -d /usr/share/fonts/wps-office ] ; then
		cd /usr/share/fonts/wps-office
		mkfontscale
		mkfontdir
		fc-cache -f
	fi
}

function ks_config()
{
	ks_config_menu	
	ks_config_fonts
}

function ks_remove()
{
	if [ -e /etc/xdg/menus/applications-merged/wps-office.menu ] ; then
		rm -rf /etc/xdg/menus/applications-merged/wps-office.menu
	fi

	if [ -x /usr/bin/update-mime-database ] ; then
		update-mime-database "${ksv_xdg_dir}/mime"
	fi

	if [ -x /usr/bin/update-desktop-database ] ; then
		update-desktop-database -q "${ksv_xdg_dir}/applications"
	fi

	if [ -d /usr/share/fonts/wps-office ] ; then
		cd /usr/share/fonts
		fc-cache -f
	fi
}

function ks_purge()
{
	if [ -d /usr/share/fonts/wps-office ] ; then
		rm -rf /usr/share/fonts/wps-office
	fi
}

function ks_uninstall_icon()
{
	local context=$1
	shift
	local mode=$1
	shift

	local png=
	local mime=
	local nextIsPng=0
	for item in $@
	do
		if [ "" = "${item}" ] ; then
			continue
		fi
		if [ ${nextIsPng} -eq 1 ] ; then
			png=${item}
			nextIsPng=0
		else
			mime=${item}
			for i in 48 32 22 16; do
				if [ -e "${ksv_xdg_dir}/${ksv_def_icon_theme}/${i}x${i}/${context}/${png}" ] ; then
					xdg-icon-resource uninstall --noupdate --mode ${mode} --context ${context} --size ${i} ${mime}
				fi
			done

			nextIsPng=1
		fi
	done
}


function ks_prerm_uninstall_menu()
{
	if [ -f "${ksv_xdg_dir}/applications/wps-office-et.desktop" ] ; then
		xdg-mime uninstall --mode system "${ksv_xdg_dir}/mime/packages/wps-office-et.xml"

		#xdg-desktop-menu uninstall --noupdate --mode system "${ksv_xdg_dir}/desktop-directories/wps-office.directory" "${ksv_xdg_dir}/applications/wps-office-et.desktop"
		xdg-desktop-menu uninstall --noupdate --mode system "${ksv_xdg_dir}/applications/wps-office-et.desktop"
		xdg-desktop-menu forceupdate --mode system

		ks_uninstall_icon "mimetypes" "system" "${ksv_et_mimes[*]}" "${ksv_excel_mimes[*]}"
		xdg-icon-resource forceupdate --mode system
	fi

	if [ -f "${ksv_xdg_dir}/applications/wps-office-wpp.desktop" ] ; then
		xdg-mime uninstall --mode system "${ksv_xdg_dir}/mime/packages/wps-office-wpp.xml"

		#xdg-desktop-menu uninstall --noupdate --mode system "${ksv_xdg_dir}/desktop-directories/wps-office.directory" "${ksv_xdg_dir}/applications/wps-office-wpp.desktop"
		xdg-desktop-menu uninstall --noupdate --mode system "${ksv_xdg_dir}/applications/wps-office-wpp.desktop"
		xdg-desktop-menu forceupdate --mode system

		ks_uninstall_icon "mimetypes" "system" "${ksv_wpp_mimes[*]}" "${ksv_ppt_mimes[*]}"
		xdg-icon-resource forceupdate --mode system
	fi

	if [ -f "${ksv_xdg_dir}/applications/wps-office-wps.desktop" ] ; then
		xdg-mime uninstall --mode system "${ksv_xdg_dir}/mime/packages/wps-office-wps.xml"

		#xdg-desktop-menu uninstall --noupdate --mode system "${ksv_xdg_dir}/desktop-directories/wps-office.directory" "${ksv_xdg_dir}/applications/wps-office-wps.desktop"
		xdg-desktop-menu uninstall --noupdate --mode system "${ksv_xdg_dir}/applications/wps-office-wps.desktop"
		xdg-desktop-menu forceupdate --mode system

		ks_uninstall_icon "mimetypes" "system" "${ksv_wps_mimes[*]}" "${ksv_word_mimes[*]}"
		xdg-icon-resource forceupdate --mode system
	fi

}

function ks_prerm_upgrade()
{
	ks_prerm_uninstall_menu
}

function ks_prerm_remove()
{
	ks_prerm_uninstall_menu
}

function ks_main()
{
	if [ $# -eq 0 ] ; then
		return;
	fi

	ks_init
	case $1 in
		configure )
			shift
			ks_config $@
			;;
		prerm )
			shift
			ks_prerm_remove $@
			;;
		remove )
			shift
			ks_remove $@
			ks_purge $@
			;;
		upgrade )
			shift
			ks_prerm_upgrade $@
			ks_config $@
			;;
	esac
}

post_install()
{
	ks_main configure
}

post_upgrade()
{
	ks_main upgrade
}

pre_remove()
{
	ks_main prerm
}

post_remove()
{
	ks_main remove
}
```

* makepkg

* install

``` bash

pacman -U *.pkg.tar.xz 

```
