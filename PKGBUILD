# Maintainer: josephgbr <rafael.f.f1@gmail.com>

pkgname=teeworlds-monster
pkgver=0.6.2.20130712
pkgrel=2
pkgdesc="A customized server by Neox with bad monsters"
arch=('x86_64' 'i686')
url="https://www.teeworlds.com/forum/viewtopic.php?id=10413"
license=('custom') # free/opensource
depends=(teeworlds)

# ugly workaround for solidfiles interaction to get direct URL
getdirecturl() {
   curl -L $1 > page.html
   output=`grep 'id="direct-download-link"' page.html | cut -d\" -f6`
   rm page.html
   echo $output
}

source=(server.sh.in monster-srv.cfg ctf5_easy.map ctf5_monster.map ktm5.map monster_rain.map monster_world.map)
source_x86_64=("teeworlds-monster_srv-${pkgver}-64bit::`getdirecturl http://www.solidfiles.com/d/a7e8a8ebd4/`")
source_i686=("teeworlds-monster_srv-${pkgver}-32bit::`getdirecturl http://www.solidfiles.com/d/42c88a32d3/`")
md5sums=('529146a3b13993770fa414f66c67fa26'
         '0d8a00d037d2274e424c4e40fedc7a43'
         'd4e7a5f167fc96fb4b1755eb72ce705c'
         'cf1b721bd7b75797c331f75b68937ccd'
         '10def7d461d6bb8a83e3bca10e2a002d'
         '237079fe2b633bc8b2e447e5183a407f'
         'c56f4adaeccaab7557840b48c19da013')
md5sums_x86_64=('05d645fe0e63cf6cf1b1d5db77f8df00')
md5sums_i686=('88dad314f6510ad26762824510536a5e')

package() {
  install -Dm755 teeworlds-monster_srv-${pkgver}-* "$pkgdir"/usr/share/$pkgname/teeworlds_srv
  
  install -Dm644 monster-srv.cfg "$pkgdir"/usr/share/$pkgname/server.cfg
  install -Dm755 "$srcdir"/server.sh.in "$pkgdir"/usr/bin/${pkgname}_srv
  sed -i "s/@MODNAME@/$pkgname/" "$pkgdir"/usr/bin/${pkgname}_srv
  
  install -dm755  $pkgdir/usr/share/teeworlds/data/maps/
  for map in ctf5_easy ctf5_monster ktm5 monster_rain monster_world; do
    install -Dm644 $map.map "$pkgdir/usr/share/teeworlds/data/maps/"
  done
}
