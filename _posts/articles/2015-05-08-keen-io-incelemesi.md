---
layout: post
title: "Keen IO İncelemesi"
excerpt:
categories: articles
tags: [keen, event]
modified:
image:
  feature:
comments: true
share: true
author: dilara
---

**Keen IO**, mantıksal analiz için kullanılan bir servistir. Yapılan iş kısaca şöyledir; veriler herhangi bir platformdan
servise gönderilir, servis tarafından tutulur ve servis API’si ile istenilen şekilde sorgulanır.

**Event verisi:** Normalize ve ilişkisel olmayan, yapısallığı düşük, belirli bir eyleme bağlı her şeyi ifade eden veri
olarak ifade edilebilir. Bir sistemdeki kullanıcı aktiviteleri event versine örnek olarak gösterilebilir.

**Artıları;**

- SaaS (Software-as-a-Service) tabanlı bir sistemdir. Yani, servis sağlayıcılar tarafından sunulmaktadır, müşteri olarak
sunucu kiralama, işletme vs. maliyetlerden kurtulmak ve sadece ihtiyaç kadar olanı için düşük maliyetli ama kaliteli
hizmet almayı sağlamaktadır.
- Kullanılabilir yazılım geliştirme kitleri (SDK) zengindir; Python, Ruby, cURL, JavaScript, iOS, Android, Java, Node, PHP, ...
- Her türlü event verisi için kullanıma uygun olduğu düşünülmektedir.
- Kullanım kolaylığına sahiptir, hızlıdır. En basit şekilde yapılacak işlemler; kullanılacak geliştirme kiti için gerekli
Gem/Paket kurulumu, anahtarların tanımlanması ve verinin gönderilmesi.
- Veriler JSON formatında tutulmaktadır. Bu durum daha kolay gönderim yapılmasını sağlamaktadır. SQL tabanlı (Örneğin;
Google BigQuery, RedShift) bir sistemde basit bir veri gönderimi için hazırlanması gereken betik çok daha uzun ve
karmaşıktır, SQL bilgisi gerektirmektedir.

**Eksileri;**

- Verilerinin JSON formatında tutulması, verilerin SQL tabanlı bir sistemdeki gibi normalize formatta olmayacağını göstermektedir.
- Her türlü veri için değil yalnızca event formatında veriler için uygundur.

Sonuç olarak; saklanmak istenen verinin event formatında olduğu ve kolay, hızlı işlem yapmanın önemli olduğu sistemlerde tercih
edilebilecek bir servis olduğu söylenilebilir.

**Keen IO** hakkında daha fazla bilgi için: [https://keen.io/](https://keen.io/)
