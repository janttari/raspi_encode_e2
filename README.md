# raspi_encode_e2
Transcode live stream from enigma2 to HLS-stream with Raspberry Pi

First install Raspbian Buster (lite) and then this:
sudo ./asenna_asenna_fserver_*

asennusohjelma lataa tarvittavat paketit ja jyraa surutta yli nginxin yms asetukset, joten kokeile tata omalla muistikortillaan (tai pura ohjelmat kasin)

Kun Raspberry on asennettu ja rebootattu, sita voidaan pyytaa transkoodaamaan /etc/kanavat.list ekassa sarakkeessa mainittu kanava:
vlc 'http://192.168.1.23/stream.cgi?input=10'

Streamauksessa on mahdollista kayttaa useampia ulostulokanavia, toisinsanoen eri kanavien transkoodauksia voi olla kaytossa 10 kpl
vlc 'http://192.168.1.23/stream.cgi?input=10&output=5'
vlc 'http://192.168.1.23/stream.cgi?input=12&output=1'
jne
streamit muodostuu /tmp/hls/<numero> -hakemistoon, josta nginx niita palvelee eteenpain.

/etc/kanavat.list:
id|name|ffmpeg-command
id on se tunnus, jolla kanavaa pyydetaan.
nimi on vapaavalintainen nimi, jota ei nyt kayteta mihinkaan mutta sen on listalla helpottamaan muokaamista
soittokomento on se varsinainen ffmpegin suorittama komento. ffmpeg suorittaa sen muodossa:
ffmpeg <soittokomento> /ulostulohakemisto. Eli ulostulohakemistoa ei itse tassa maaritella.


/tmp/fstiimaaloki sisaltaa jonkinlaista dataa mita ohjelma on tehnyt.

skripti /usr/bin/fsvalvo valvoo etta luoduille striimeille on kysyntaa. Jos kukaan ei luotua striimia katso, se tapetaan pois.
