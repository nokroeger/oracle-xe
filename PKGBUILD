# Maintainer: Nils Oliver Kröger <me@nokroeger.de>
# Based on oracle-xe AUR by Maxim Kurnosenko <asusx2@mail.ru>
# https://aur.archlinux.org/packages/oracle-xe/
pkgname=oracle-xe
pkgver=18.1.0_1.0
pkgrel=4
pkgdesc="a non free (as in free speech) DBMS"
url="http://www.oracle.com/"
license=('custom')
arch=('x86_64')
conflicts=('oracle-xe')
provides=('oracle-xe')
options=('!strip')
depends=('libaio>=0.3.104' 'gcc>=4.1.2' 'binutils>=2.16.91.0.5' 'make>=3.80' 'glibc>=2.3.4-2.41' 'bc' 'net-tools')
install='oracle.install'
source=(
	'https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-18c-1.0-1.x86_64.rpm'
	'oracle_env.csh'
	'oracle_env.sh'
	'oracle-xe-18c'
	'oracle-xe-18c.conf'
	'oracle-xe-18c.service'
)

md5sums=(
	    '56af7b3b58abdee310aa74f8f88e16ad'
        '66416a216ac1f7597f72c6b7aee48ac3'
        'dc3e9d178c4245d0e990051093a92483'
        'aa34ee979436abe21013c0e88b3e9e93'
        'eec78d5e1551355120d06a3796b63e70'
        'c494d521fd59a1f88bec7a181f28bd82'
)

build() {
    cd $srcdir
}

package() {
    cd $srcdir

    #ammend oracle-xe-18c init.d script
    mkdir -p $srcdir/etc/init.d
    cp $srcdir/oracle-xe-18c $srcdir/etc/init.d/
    chmod +x $srcdir/etc/init.d/oracle-xe-18c

    #Let the LICENSE for this packages reflect the oracle license
    mkdir -p $srcdir/usr/share/licenses/custom/$pkgname
    cp $srcdir/usr/share/doc/oracle-xe-18c/LICENSE $srcdir/usr/share/licenses/custom/$pkgname    

    # Export environment variables
    mkdir -p $srcdir/etc/profile.d
    cp $srcdir/oracle_env.* $srcdir/etc/profile.d/
    chmod +x $srcdir/etc/profile.d/oracle_env.*

    # LD_LIBRARY_PATH
    #mkdir -p $srcdir/etc/ld.so.conf.d/
    #cp $srcdir/oracle-xe-18c.conf $srcdir/etc/ld.so.conf.d/

    # For systemd
    mkdir -p $srcdir/etc/systemd/system
    cp $srcdir/oracle-xe-18c.service $srcdir/etc/systemd/system    

    #Copy the files from the RPM
    cp -R $srcdir/opt $pkgdir/
    cp -R $srcdir/usr $pkgdir/
    cp -R $srcdir/etc $pkgdir/

    find $pkgdir/opt -exec chmod 755 {} \;
}
