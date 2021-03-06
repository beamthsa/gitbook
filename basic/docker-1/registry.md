---
description: "แหล่งเก็บ Docker Images ที่ใหญ่ที่สุดในโลก \U0001F60D"
---

# 🗃️ Docker Registry

🤠 จาก [**บทความที่ 3**](https://www.saladpuk.com/basic/docker-1/exercise01) ****กับ ****[**บทความที่ 4**](https://www.saladpuk.com/basic/docker-1/tools) ที่ได้ลองเล่น **`🐳 Docker`** เราจะพบว่ามันมีขั้นตอนหนึ่งที่พูดถึง **`🗃️ Docker Registry`** รวมอยู่ด้วย ซึ่งจะไม่พูดถึงก็ไม่ได้ เพราะมันเป็นหนึ่งในหัวใจของพี่วาฬน้ำเงินของเราเลยทีเดียว ดังนั้นในบทความนี้เราจะมาลงรายละเอียดกับ **`🗃️ Docker Registry`** กันฮ๊าฟ

{% hint style="success" %}
**แนะนำให้อ่าน**  
บทความนี้เป็นส่วนหนึ่งของคอร์ส [🐳 **Docker**](https://www.saladpuk.com/basic/docker-1) ที่จะสอนตั้งแต่เรื่องพื้นฐานยันระดับ master กันไปเลย ซึ่งเนื้อหาทั้งหมดจะทำให้เพื่อนๆเข้าใจและใช้งาน **Docker** โดยใช้ **Kubernetes** เป็น และสามารถสร้าง **Cluster** เพื่อนำไปใช้งานบน **Cloud Providers** ต่างๆได้ และทั้งหมดที่พูดมานั้นอ่านได้ฟรีเลย ดังนั้นหากสนใจก็สามารถกดเจ้าวาฬสีน้ำเงินเพื่อไปอ่านตั้งแต่เริ่มต้นได้ครัช 🤠
{% endhint %}

## 🚨 เท้าความเดิม

จาก [**บทความที่ 3**](https://www.saladpuk.com/basic/docker-1/exercise01#docker-pull) ตอนที่เราใช้คำสั่ง **`docker pull`** หรือ **`docker run`** ตัวพี่วาฬ **`🐳 Docker`** จะไปตรวจว่าในเครื่องของเรามี **`🖼️ Container Image`** นั้นๆอยู่หรือเปล่า ซึ่งหากไม่มีเขาก็จะไปดาวโหลดมาจาก **`🗃️ Docker Registry`** มาเก็บไว้ในเครื่องตามรูปด้านล่าง

![](../../.gitbook/assets/image%20%281137%29.png)

🤠 ตรงจุดนี้จะทำให้เรารู้คร่าวๆละว่า **`🗃️ Docker Registry`** คือแหล่งเก็บ **`🖼️ Container Images`** ที่อยู่บนอินเตอร์เน็ตนั่นเอง ดังนั้นเราจะลองซูมเข้าไปดูว่าข้างในนั้นมันเป็นยังไงบ้างดีกว่า

## 🗃️ Docker Registry

ถ้าจะอธิบายตรงนี้ **ดช.แมวน้ำ** อยากให้จินตนาการถึงตอนที่เราเขียนโปรแกรม แล้วอยากเอา package ของคนอื่นที่อยู่บนอินเตอร์เน็ตมาใช้ เราก็จะไปดาวโหลด package พวกนั้นมาจากส่วนกลางของแต่ละภาษา เช่น [`nuget`](https://www.nuget.org/), [`nodejs`](https://nodejs.org/), [`pip`](https://pypi.org/), [`bower`](https://bower.io/) บลาๆ มาติดตั้งที่โปรเจคของเราชิมิ

จากแนวคิดที่ว่ามาเจ้า **`🐳 Docker`** ก็มีตัวกลางที่เอาไว้เก็บ **`🖼️ Container Images`** ของทุกคนทั่วโลกเช่นกัน ดังนั้นเมื่อมีคนสร้าง **`🖼️ Container Image`** แล้วอยากจะแชร์ให้คนในทีม/ทั่วโลกใช้ เขาก็จะทำการอัพโหลดมันขึ้นมาเก็บที่ **`🗃️ Docker Registry`** นั่นเอง ดังนั้นเวลาที่เราใช้คำสั่งที่เกี่ยวข้องกับ Image แล้วพี่วาฬมองหา Image ในเครื่องไม่เจอ เขาก็จะว่ายน้ำไปตามหา Image ตัวนั้นๆจาก **`🗃️ Docker Registry`** มาให้เรานั่นเอง ตามรูปด้านล่าง

![](../../.gitbook/assets/image%20%281170%29.png)

🤠 โดยปรกติถ้าเราพูดคำว่า **`🗃️ Docker Registry`** มันจะหมายถึง [**`🌎 Docker Hub`**](https://hub.docker.com/) ที่เป็นตัวรวม **`🖼️ Container Images`** ของทุกคนทั่วโลก ซึ่งมันมี Container Image อยู่ในนั้นเป็น 1,000,000,000 ล้านตัว+ และมีผู้ใช้เงินเกิน 5 ล้านคนต่อวัน 🤯 ดังนั้นของแทบจะทุกอย่างที่เราอยากได้เกิน 80% น่าจะอยู่บนนั้นหมดแล้วนั่นเอง

![https://hub.docker.com](../../.gitbook/assets/image%20%281169%29.png)

โดยปรกติถ้าเราจะสร้าง **`🖼️ Container Image`** ไปฝากไว้บน **`🌎 Docker Hub`** เราก็สามารถทำได้เลยแถมฟรีด้วย แต่ข้อเสียของมันคือ **👁️ ทุกคนบนโลกมองเห็นและสามารถใช้งานได้นะจ๊ะ** \(ก็เหมือนฝากโค้ดไว้กับ Git Hub งุย\) ซึ่งถ้าเราไม่อยากให้คนอื่นเห็น เช่นงานเราสำคัญมากๆไรงี้ เราต้องจ่ายเงินเพื่อทำเป็น private นั่นเอง

{% hint style="warning" %}
**คำเตือน**  
เราสามารถสร้าง private container image ได้ฟรี 1 อันต่อ 1 account ก็จริง แต่กฎใหม่ของ Docker Hub ที่พึ่งออกมาสดๆร้อนได้บอกว่า **ถ้า Container Image ไม่มีการเคลื่อนไหวนานเกิน 6 เดือน มันจะถูกลบอัตโนมัติ** ดังนั้นให้ระวังไว้ด้วยนะจ๊ะ
{% endhint %}

## 🗃️ Container Registry

ถ้าถามว่ามันมีที่เก็บ **`🖼️ Container Images`** แค่ใน **`🌎 Docker Hub`** เพียงที่เดียวหรือเปล่า? คำตอบคือไม่ใช่ เพราะทั่วโลกมีผู้ให้บริการเก็บ Container Image อยู่มากมาย โดยเฉพาะกับเหล่าผู้ให้บริการคลาว์ด ไม่ว่าจะเป็น **Microsoft** ก็มี [**ACR \(Azure Container Registry\)**](https://azure.microsoft.com/en-us/services/container-registry/) ส่วน **Amazon** ก็มี [**ECR \(Elastic Container Registry\)**](https://aws.amazon.com/ecr/) พี่ **Google** ก็มี [**CR \(Container Registry\)**](https://cloud.google.com/container-registry) และพี่จีน **Alibaba** ก็มี [**CR \(Container Registry\)**](https://www.alibabacloud.com/product/container-registry) ให้เราได้ลองเลือกใช้กัน 😉

![](../../.gitbook/assets/image%20%281168%29.png)

> รายละเอียดการเอา **`🖼️ Container Image`** ไปเล่นกับผู้ให้บริการคลาว์ดแต่ละเจ้าได้เห็นแน่นอนแต่ **ดช.แมวน้ำ** ขอแยกเอาไว้โชว์ในบทความถัดๆไปนะขอรับ

{% hint style="success" %}
**เกร็ดความรู้**  
ไม่ว่าเราจะใช้บริการฝาก **`🖼️ Container Images`** ไว้กับผู้ให้บริการรายไหนก็ตามก็ไม่ต้องเป็นกังวล เพราะ **🗃️ Container Registry ทุกเจ้าสามารถใช้งานร่วมกันได้หมดเบย 💖**
{% endhint %}

## 🎯 Summary

**`🗃️ Docker Registry`** คือส่วนกลางที่เอาไว้เก็บ **`🖼️ Container Image`** จากทั่วโลกไว้บนอินเตอร์เน็ต ซึ่งรู้จักกันในชื่อ **`🌎 Docker Hub`** นั่นเอง แต่ก็ยังมีที่เก็บ **`🖼️ Container Image`** อื่นๆทั่วโลก เช่นจากผู้ให้บริการคลาว์ดอย่าง **Microsoft**, **Amazon**, **Google** และ **Alibaba** คอยให้เราได้ลองใช้บริการอยู่นั่นเอง

{% hint style="info" %}
**หมายเหตุ**  
รายละเอียดของ **`🗃️ Docker Registry`** จริงๆยังมีอีกเยอะเบยที่น่าสนใจ แต่ถ้าเราจะอัดแต่ทฤษฎีเพียงอย่างเดียวก็จะเข้าใจมันได้ไม่เต็มร้อย ดังนั้น **ดช.แมวน้ำ** จะค่อยๆอธิบายควบคู่กับตอนทำ Workshop ละกันนะจุ๊ฟๆ 😙
{% endhint %}

ในบทความถัดไปเดี๋ยวเรามาลองสร้าง **`🖼️ Container Image`** ตัวแรกของเรา เพื่อเอาไปใช้งานส่วนตัว หรือ เอาไปใช้ภายในทีมกันครัช

{% page-ref page="images.md" %}

{% hint style="success" %}
อ่านแล้วชอบป๋มก็ขอฝากแชร์ หรือกดติดตามเพื่อจะได้ไม่พลาดบทความอื่นๆจาก **ดช.แมวน้ำ** ได้จากลิงค์นี้เบยครัช [**Saladpuk Fanclub**](https://www.facebook.com/mr.saladpuk/?modal=admin_todo_tour) **😍**
{% endhint %}

![&#xE0A;&#xE48;&#xE2D;&#xE07;&#xE17;&#xE32;&#xE07;&#xE2A;&#xE19;&#xE31;&#xE1A;&#xE2A;&#xE19;&#xE38;&#xE19;&#xE04;&#xE48;&#xE32;&#xE2D;&#xE32;&#xE2B;&#xE32;&#xE23;&#xE41;&#xE21;&#xE27;&#xE19;&#xE49;&#xE33;&#xE01;&#xE31;&#xE4A;&#xE1F; &#x1F618;](../../.gitbook/assets/promptpay.png)

