# Jarkom_Modul3_Lapres_A03

## Soal 1

Untuk membuat topologi seperti pada soal shift, maka pada topologi.sh kita bisa ganti menjadi seperti dibawah, dengan ada tambahan switch 3, klient madiun dan banyuwangi, serta server tuban.
```
# Switch
uml_switch -unix switch1 > /dev/null < /dev/null &
uml_switch -unix switch2 > /dev/null < /dev/null &
uml_switch -unix switch3 > /dev/null < /dev/null &

# Router
xterm -T SURABAYA -e linux ubd0=SURABAYA,jarkom umid=SURABAYA eth0=tuntap,,,'10.151.72.17' eth1=daemon,,,switch1 eth2=daemon,,,switch3 eth3=daemon,,,switch2 mem=256M &

# Server
xterm -T MALANG -e linux ubd0=MALANG,jarkom umid=MALANG eth0=daemon,,,switch2 mem=160M &
xterm -T MOJOKERTO -e linux ubd0=MOJOKERTO,jarkom umid=MOJOKERTO eth0=daemon,,,switch2 mem=128M &
xterm -T TUBAN -e linux ubd0=TUBAN,jarkom umid=TUBAN eth0=daemon,,,switch2 mem=128M &

# Klien Subnet 1
xterm -T SIDOARJO -e linux ubd0=SIDOARJO,jarkom umid=SIDOARJO eth0=daemon,,,switch1 mem=64M &
xterm -T GRESIK -e linux ubd0=GRESIK,jarkom umid=GRESIK eth0=daemon,,,switch1 mem=64M &

# Klien Subnet 2
xterm -T BANYUWANGI -e linux ubd0=BANYUWANGI,jarkom umid=BANYUWANGI eth0=daemon,,,switch3 mem=64M &
xterm -T MADIUN -e linux ubd0=MADIUN,jarkom umid=MADIUN eth0=daemon,,,switch3 mem=64M &
```

Setelah kita bash topologi.sh, kita ketikan `nano /etc/sysctl.conf` dan uncomment pada `net.ipv4.ip_forward=1`, lalu save dan ketikkan command `sysctl -p` untuk mengaktifkan perubahan yang ada.

Lalu, kita setting IP dari UML dengan `nano /etc/network/interfaces`.

**UML Surabaya:**

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.72.18
netmask 255.255.255.252
gateway 10.151.72.17

auto eth1
iface eth1 inet static
address 192.168.0.1
netmask 255.255.255.0

auto eth2
iface eth2 inet static
address 192.168.1.1
netmask 255.255.255.0

auto eth3
iface eth3 inet static
address 10.151.73.33
netmask 255.255.255.248
```

**UML Malang:**

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.73.34
netmask 255.255.255.248
gateway 10.151.73.33
```

**UML Mojokerto:**

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.73.35
netmask 255.255.255.248
gateway 10.151.73.33
```

**UML Tuban:**

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
address 10.151.73.36
netmask 255.255.255.248
gateway 10.151.73.33
```

## Soal 2

## Soal 3

## Soal 4

## Soal 5
## Soal 6

## Soal 7

## Soal 8

## Soal 9

## Soal 10

## Soal 11

## Soal 12
