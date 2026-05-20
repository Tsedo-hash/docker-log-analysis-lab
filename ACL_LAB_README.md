from pathlib import Path

content = """# ACL тохируулах лабораторийн ажил

## Лабораторийн ажлын зорилго

Энэхүү лабораторийн ажлаар **Standard ACL**, **Extended ACL** болон **Named Extended ACL** тохируулна.  
Оюутан ACL-ийг зөв interface дээр зөв чиглэлтэйгээр байрлуулж, тохиргооны үр дүнг `ping`, `web browser`, `show access-lists`, `show running-config` командуудаар баталгаажуулах чадварт суралцана.

---

## Scenario

Өгөгдсөн топологид буй төхөөрөмжүүдийн IP хаяглалтыг хийсэн бөгөөд **Router0** болон **Router1** төхөөрөмжүүд дээр **static routing** тохируулсан гэж үзнэ.

Хандалтыг зохицуулах зорилгоор дараах даалгавруудад өгөгдсөн шаардлагын дагуу ACL тохируулна.

---

## Топологи

**Зураг 5.1. Даалгаврын топологи**

> Энэ хэсэгт Packet Tracer-ийн топологийн зургийг оруулна.

---

## IP хаяглалт

**Хүснэгт 5.1. IP хаяглалт**

| Төхөөрөмж | IP address | Subnet mask | Gateway | Interface |
|---|---:|---:|---:|---|
| Admin PC | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 | Fa0 |
| Student PC | 192.168.10.20 | 255.255.255.0 | 192.168.10.1 | Fa0 |
| Guest PC | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 | Fa0 |
| Web Server | 192.168.30.10 | 255.255.255.0 | 192.168.30.1 | Fa0 |
| Internal Server | 192.168.40.10 | 255.255.255.0 | 192.168.40.1 | Fa0 |
| Router0 | 192.168.30.1 | 255.255.255.0 | - | G0/0 |
| Router0 | 192.168.10.1 | 255.255.255.0 | - | G0/1 |
| Router0 | 10.0.0.1 | 255.255.255.252 | - | G0/2 |
| Router1 | 192.168.40.1 | 255.255.255.0 | - | G0/0 |
| Router1 | 192.168.20.1 | 255.255.255.0 | - | G0/1 |
| Router1 | 10.0.0.2 | 255.255.255.252 | - | G0/2 |

---

# Даалгавар 1: Standard ACL тохируулах

## Шаардлага

**Web Server-ээс Guest PC лүү хандалт хийхийг хориглоно.**

- ACL дугаар: `10`
- Guest PC → Web Server ping амжилтгүй байх ёстой.
- Admin PC → Web Server ping амжилттай байх ёстой.
- Student PC → Web Server ping амжилттай байх ёстой.

## Тайлбар

Standard ACL нь зөвхөн **source IP address**-ийг шалгадаг.  
Иймээс Standard ACL-ийг destination буюу очих сүлжээнд ойр байрлуулах нь тохиромжтой.

## Жишээ тохиргоо

```bash
Router0(config)# access-list 10 deny 192.168.20.10 0.0.0.0
Router0(config)# access-list 10 permit any
Router0(config)# interface g0/0
Router0(config-if)# ip access-group 10 out
