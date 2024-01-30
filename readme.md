# Time capsule API

## Proyekt haqqında

Bu proyekt vasitəsilə, FutureMe.org kimi bir saytın backendini hazırlamalıyıq. Bu saytdakı əsas məqsəd, istfadəçilərin gələcəyə bir məktub yaza bilməsi və seçdikləri tarixdə emailləri çatmış olmasıdır.

## Əsas özəlliklər

### 1) İstifadəçi qeydiyyatı/girişi:

> Bu özəlliklə, istifadəçilər özlərinə hesab aça və həmin hesaba login edə bilərlər. Hesab açılarkən onlara təsdiq mesajı getməlidir və yalnız bundan sonra onların hesabı aktiv olmuş olur. Aşağıdakı kimi endpointlər ola bilər:

- `POST: api/auth/register`
- `POST: api/auth/login`
- `GET: api/auth/verify?token:string&email:string`
- `POST: api/auth/resetPass`

### 2) Zaman kapsulları:

> Bu bölmə ilə, istifadəçi yeni zaman kapsulları yarada bilər, bu kapsullara istəsə hansısa fayl(mətn və ya şəkil kimi) və ya bir başa email yaza bilər hətta istəsə hər ikisini də əlavə edə bilməlidir. Beləliklə, nümunə endpointlər aşağıdakı kimi ola bilər:

- `GET: api/userCapsules?page:int` -> bütün kapsullarına baxa bilməli
- `GET: api/userCapsules/{capsuleId}` -> sadəcə birinə baxacaq
- `POST: api/userCapsules` -> yeni kapsul yaradır
- `PUT: api/userCapsules/{capsuleId}` -> hansısa kapsul üzərində dəyişiklik edir
- `PATCH: api/userCapsules/{capsuleId}` -> hansısa kapsulun bir məlumatlarının bir qismini dəyişir
- `DELETE: api/userCapsules/{capsuleId}` -> kapsulu silir

> Əlavədən olaraq, bu kapsullara müəyyən vaxtdan sonra artıq `GET: api/userCapsules/{capsuleId}` endpoint-i işləməməlidir, çünki onda əsas məqsədini itirmiş olur. Və onu qeyd edək ki, bu özünə aid olan kapsullar idi və bu endpointlər JWT token ilə authentication istəməlidir.

### 3) Global kapsullar:

> Global kapsullar isə, insanların hər kəsə açıq paylaşdıqları kapsullardır, və bunlara digər insanlar baxa bilməli istəsə yaddaşa almalı,bəyənə bilməlidir.

- `GET: api/timeCapsules?page:int` -> bütün kapsullara baxa bilər
- `GET: api/timeCapsules/{capsuleId}` -> sadəcə birinə baxacaq
- `GET: api/comments/{capsuleId}?page:int` -> spesifik kapsulun kommentləri gəlməlidir
- `POST: api/comments/{capsuleId}` -> hansısa kapsula yeni komment əlavə etmək
- `PATCH: api/timeCapsules/{capsuleId}` -> bununla isə kapsulun like sayını artırmaq olar

> ❗ Bu endpointlər nümunə məqsədlidir, artırıla bilər(ancaq çalışın azaltmayın🤠).

### 4) Əlavə qeyd və araşdırma mövzusu:

> Bu API hər gün olan vaxt ilə databazada olan kapsulları yoxlamalı və vaxtı çatıbsa lazımi ünvana(və ya ünvanlara) göndərməlidir. Bunun üçünsə background jobları(taskları) araşdıra bilərsiniz. Bunu [ASP.NET](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/host/hosted-services?view=aspnetcore-8.0&tabs=visual-studio) in özü ilə də və ya [Quartz](https://www.quartz-scheduler.net/) kimi kitabxanalarla da edə bilərsiniz
