# مشروع SE4111 - Student Grade API مع CI/CD

## محتويات المشروع
- Spring Boot REST API لإدارة بيانات الطلاب.
- ثلاث اختبارات JUnit.
- تسجيل أحداث باستخدام SLF4J وLog4j2.
- Dockerfile متعدد المراحل.
- GitHub Actions workflow للبناء والاختبار وفحص SonarQube والنشر إلى Docker Hub.

## قبل التشغيل
ثبّت Java 17 أو أحدث، وMaven 3.8+، وGit، وDocker Desktop. تحتاج كذلك حسابات GitHub وDocker Hub وSonarQube Cloud.

## تشغيل الاختبارات محليًا
```bash
mvn clean test
```

## تشغيل التطبيق محليًا
```bash
mvn spring-boot:run
```
ثم افتح:
- http://localhost:8080/api/students
- http://localhost:8080/api/students/1
- http://localhost:8080/api/health

## إعداد SonarQube
في `pom.xml` استبدل:
- `YOUR-SONAR-ORG` بمفتاح المؤسسة (Organization key).
- `YOUR-SONAR-PROJECT-KEY` بمفتاح المشروع (Project key).

## إعداد GitHub Actions Secrets
أضف هذه القيم من:
Repository → Settings → Secrets and variables → Actions

- `DOCKERHUB_USERNAME`: اسم مستخدم Docker Hub.
- `DOCKERHUB_TOKEN`: رمز Docker Hub، وليس كلمة المرور.
- `SONAR_TOKEN`: رمز SonarQube Cloud.

لا تضع أي token أو كلمة مرور داخل ملفات المشروع أو GitHub commits.

## بناء وتشغيل Docker محليًا
```bash
docker build -t student-grade-api:local .
docker run -d -p 8080:8080 --name grades student-grade-api:local
```
افتح http://localhost:8080/api/health

لإيقاف الحاوية وحذفها:
```bash
docker stop grades
docker rm grades
```

## ملاحظة
تم تضمين endpoint `/api/health` والاختبار الخاص به مسبقًا لتسهيل التحقق النهائي. في عرض المشروع اشرح أنه يمثل النشاط النهائي في دليل المختبر.
