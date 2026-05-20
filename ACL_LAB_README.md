ACL тохируулах лабораторын ажил 

Энэхүү лабораторийн ажлаар Standard ACL, Extended ACL болон Named Extended ACL тохируулна. ACL-ийг зөв interface дээр зөв чиглэлтэйгээр байрлуулж, үр дүнг баталгаажуулах чадварт суралцана. 

Scenario 

Өгөгдсөн топологид буй төхөөрөмжүүдийн хаяглалтыг ба Router0 болон Router1 төхөөрөмжүүд дээр static routing тохируулсан. Хандалтыг зохицуулах зорилгоор даалгавруудад өгөгдсөн шаардлагын дагуу ACL тохируул.  

Топологи: 

Зураг 5.1. Даалгаврын топологи 

IP хаяглалт 

Төхөөрөмж 

IP address 

Subnet mask 

Gateway 

Interface 

Admin PC 

192.168.10.10 

255.255.255.0 

192.168.10.1 

Fa0 

Student PC 

192.168.10.20 

255.255.255.0 

192.168.10.1 

Fa0 

Guest PC 

192.168.20.10 

255.255.255.0 

192.168.20.1 

Fa0  

Web Server 

192.168.30.10 

255.255.255.0 

192.168.30.1 

Fa0 

Internal Server 

192.168.40.10 

255.255.255.0 

192.168.40.1 

Fa0 

Router0 

192.168.30.1 

255.255.255.0 

x 

G0/0 

192.168.10.1 

255.255.255.0 

x 

G0/1 

10.0.0.1 

255.255.255.252 

x 

G0/2 

Router1 

192.168.40.1 

255.255.255.0 

x 

G0/0 

192.168.20.1 

255.255.255.0 

x 

G0/1 

10.0.0.2 

255.255.255.252 

x 

G0/2 

Хүснэгт 5.1. IP хаяглалт 

Даалгавар 1: Standard ACL тохируулах 

Web Server-ээс Guest PC лүү хандалт хийхийг хоригло. 

ACL дугаар: 10 

Guest PC - Web Server ping амжилтгүй байх ёстой. 

Admin PC - Web Server ping амжилттай байх ёстой. 

Student PC - Web Server ping амжилттай байх ёстой. 

Даалгавар 2: Extended ACL тохируулах 

Student PC буюу 192.168.10.20 хаягтай төхөөрөмж Internal Server буюу 192.168.40.10 рүү ping хийх боломжгүй байна. Гэхдээ Internal Server-ийн HTTP service рүү web browser ашиглан хандаж чаддаг байх. 

ACL дугаар: 100 

ICMP traffic-ийг хориглоно. 

HTTP буюу TCP port 80 traffic-ийг зөвшөөрнө. 

Student PC - Internal Server ping амжилтгүй байх ёстой. 

Student PC - http://192.168.40.10  вебийн хандалт амжилттай байх ёстой. 

Даалгавар 3: Named Extended ACL тохируулах 

Server талаас хэрэглэгчийн сүлжээ рүү шууд хандах traffic-ийг хоригло. Хэрэглэгчийн талаас server тал руу хандах traffic зөвшөөрөгдсөн хэвээр байна. 

Router0 дээр BLOCK_WEB_TO_USERS нэртэй Named Extended ACL үүсгэнэ. 

Web Server network буюу 192.168.30.0/24 сүлжээнээс Admin PC буюу 192.168.10.20 төхөөрөмж рүү хандахыг хориглоно. 

Router1 дээр BLOCK_ADMIN&USER нэртэй Named Extended ACL үүсгэнэ. 

Admin болон Student PC буюу 192.168.10.10, 192.168.10.20 хаягаас Guest PC буюу 192.168.20.10 хаяг руу хандахыг хориглоно. 

Бусад traffic зөвшөөрөгдөнө. 

Шалгах командууд 

show access-lists 

show running-config 

ping 

web browser 

Бататгах асуулт 

Standard ACL юуг шалгадаг вэ? 

Extended ACL нь Standard ACL-ээс юугаараа ялгаатай вэ? 

Named ACL-ийн давуу тал юу вэ? 

Standard ACL-ийг яагаад destination-д ойр байрлуулдаг вэ? 

Extended ACL-ийг яагаад source-д ойр байрлуулдаг вэ? 

ACL-ийн implicit deny гэж юу вэ? 

ACL-ийг Interface дээр in болон out чиглэлд тавихын ялгаа юу вэ? 
