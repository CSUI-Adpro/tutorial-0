# Tutorial 0 - Memahami Spring Boot

> author: `HZZ`

Pada tutorial ini, kamu akan diajak untuk berkenalan dan memahami salah satu framework paling popoler pada bahasa pemrograman Java, yaitu Spring Boot. Spring Boot adalah framework Java yang mempermudah pembuatan aplikasi web dengan konfigurasi minimal dan fitur _production-ready_. Hal ini memudahkan proses pembuatan aplikasi web dengan menyediakan auto-configuration dan management endpoints. Dengan tutorial ini, kamu diharapkan bisa memahami tentang framework tersebut, mulai dari cara membuat proyeknya, cara kerjanya, dan cara menjalankannya.

Tutorial ini juga memuat beberapa guide lain yang bisa dibaca sebagai pengayaan:

- [git.md](git.md): berisi refresher terkait git dan beberapa konsep git tingkat lanjut yang akan kamu manfaatkan selama perkuliahan AP
- [intellij.md](intellij.md): berisi tutorial menginstall Intellij IDEA Ultimate
- [runner.md](runner.md): berisi tutorial menjalankan _gitlab runner_-mu sendiri menggunakan docker container

## Langkah-Langkah Pembuatan project Spring Boot

Prasyarat:

1. IntelliJ **Ultimate** sudah terinstall
2. Git sudah terinstall

Langkah-langkah:

1. Buka aplikasi IntelliJ Ultimate.

2. Tekan tombol "New Project".

3. Tekan menu "Spring Initializr" pada IntelliJ.

   ![step-1](https://i.imgur.com/9hIb4HZ.png)

4. Silakan isi nama project dan lokasi project sesuai preferensi kamu.

5. Pilihlah bahasa "Java", Type "Gradle - Kotlin", dan Group "id.ac.ui.cs.advprog". Untuk Artifact dan Package name, biarkan IntelliJ saja yang memberikan namanya. Untuk field `JDK` dan `Java`, kamu bisa memilih versi apapun yang **lebih besar atau sama dengan versi 17**. Pada contoh gambar di atas.

6. Tekan "Next".

7. Pilihlah spring boot versi 3.0.2, dan tambahkan _dependencies_ "Spring Boot DevTools", "Lombok", "Spring Configuration Processor", "Spring Web", dan "Thymeleaf".

   <img src="https://i.imgur.com/hXdsFsS.png" alt="image" style="zoom:50%;" />

   <br></br>

   <img src="https://i.imgur.com/kpniPVu.png" alt="image" style="zoom:50%;" />

8. Setelah itu tekan "Create".

9. Silakan menunggu sebentar sampai IntelliJ selesai menjalankan tugasnya (misal download gradle, dsb.). kamu dapat melihat perkembangannya pada bagian kanan bawah window IntelliJ.

   ![image](https://i.imgur.com/lFXgbeR.png)

10. Untuk memastikan bahwa project sudah berhasil dibuat, silakan coba jalankan project kamu dengan menekan tombol segitiga hijau (Run) pada bagian kanan atas window IntelliJ.

    <img src="https://i.imgur.com/4w56ayi.png" alt="image" style="zoom:50%;" />

11. Setelah itu, coba kunjungi `localhost:8080` pada browser kamu. Seharusnya, tampilannya akan sama seperti gambar di bawah ini.

    <img src="https://i.imgur.com/7l2lcsL.png" alt="image" style="zoom:50%;" />

Catatan tambahan:

> kamu juga dapat memanfaatkan situs [start.spring.io](https://start.spring.io/) untuk membuat project spring boot baru.

---

## Struktur Project Spring Boot

<br />

<img src="https://i.imgur.com/WMNyAu4.png" alt="image" style="zoom:50%;" /><br />

1. Folder `src`
   Pada umumnya, folder ini akan menyimpan seluruh kode-kode _logic_ aplikasi spring boot kita. Folder ini sendiri biasanya dibagi menjadi 2 folder lagi: `main` dan `test`.
   - Folder `main`
     Folder ini bertanggung jawab atas konten dan _logic_ dari aplikasi kita. Folder ini di bagi menjadi 2 lagi: `java` dan `resources`.
     - Folder `java`
       Berisi kode-kode Java (spring boot) yang bertanggung jawab atas logic dari aplikasi kita
     - Folder `resources`
       Berisi file-file pendukung dari aplikasi web kita, misalnya seperti templates (HTML), static files (CSS, JS, gambar, dll), dan `application.properties`. File `application.properties` ini berperan untuk menyimpan konfigurasi-konfigurasi aplikasi spring boot. Perannya mirip seperti file `settings.py` pada framework Django.
   - Folder `test`
     Folder ini bertanggung jawab atas kode-kode test pada aplikasi kita. Kode test merupakan kode-kode yang berfungsi untuk menguji logic dari aplikasi kita dan memastikan bahwa logic dari aplikasi kita sudah berjalan dengan baik dan tidak ada bug.
2. File `.gitignore`
   Berisi daftar file dan folder yang tidak ingin di-commit pada git.
3. File-file Gradle (`build.gradle`, `gradlew`, `gradlew.bat`, dan `settings.gradle`)
   Pada kebanyakan kasus, teman-teman tidak butuh mengotak-atik file `gradlew` dan `gradlew.bat`. Oleh karena itu, kita akan fokus kepada `build.gradle` dan `settings.gradle`.
   - File `build.gradle`
     File ini berisikan Gradle task, informasi mengenai aplikasi kita, plugin, versi java dari project spring boot kita, dan dependencies dari aplikasi kita. Apabila pada python biasanya kita menuliskan dependencies aplikasi kita pada `requirements.txt`, maka pada project Java kita menuliskannya pada file `build.gradle` ini. Namun, perlu diingat bahwa file ini juga menyimpan informasi-informasi lain, tak hanya dependencies saja.
   - File `settings.gradle`
     File ini biasanya digunakan apabila aplikasi yang dibuat bersifat multi-project (punya beberapa submodules). enjelasan selengkapnya mengenai file ini dapat di lihat pada [link ini](https://stackoverflow.com/a/47825535/7069108).

---

## Dasar Model-View-Controller pada Spring Boot

Teman-teman mungkin sudah mengenal MVT pattern (Model-View-Template) pada Django. Pada spring boot, biasanya kita akan menggunakan MVC pattern (Model-View-Controller). Pada dasarnya, MVT merupakan turunan dari MVC. Design pattern MVT ini dibuat dan disesuaikan untuk penggunaan pada Django. Perlu diperhatikan bahwa MVC dan MVT memiliki layer yang nama-nya sama, tetapi memiliki peran yang berbeda.
Berikut ini penjelasan sederhana mengenai MVC dan MVT:

- Pada MVC, `view` merupakan layer yang bertugas untuk tampilan. Sementara itu, pada MVT, peran ini dipegang oleh `template`.
- Pada MVT, `view` merupakan layer tempat diimplementasikannya logika bisnis dan request-response aplikasi. Sementara itu, pada MVC, peran request-response dipegang oleh `controller`, dan peran logika bisnis dipegang oleh `model`.

Berikut ini penjelasan lebih detail mengenai layer-layer pada MVC:

- `model`
  Layer ini bertugas untuk menyimpan implementasi logika bisnis dan representasi data. Pada spring boot, layer ini dibagi lagi menjadi 2 untuk meningkatkan _maintainability_. layer ini dibagi menjadi `service` dan `repository`. `service` merupakan layer yang bertanggung jawab atas logika bisnis. `repository` merupakan layer yang bertanggung jawab tas pengelolaan data, misalnya menyimpan dan memperoleh data dari database.
- `controller`
  Layer yang mengatur request dan response dari aplikasi ini. Layer ini tidak boleh mengandung kode yang berkaitan dengan logika bisnis. Hanya request dan response saja yang dikelola oleh layer ini.
- `view`
  Layer yang berfungsi untuk mengatur tampilan. Dapat dikatakan bahwa layer ini terdiri atas file HTML dan static files (CSS, Javascript).

---

<div align="justify">

# Dasar Request dan Response pada Spring Boot

> Author: `AUL`

Mari kita coba membuat aplikasi web sederhana. Sebelumnya, buatlah struktur proyek seperti berikut: <br>

<div align="center">
    <img src="https://i.imgur.com/A8HNcde.png" height="300">
</div>

## Controller

Pertama-tama, buatlah sebuah `controller` sederhana yang dapat mengembalikan halaman HTML.

`BaseController.java`

```java
package id.ac.ui.cs.advprog.tutorial0.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

@Controller
public class BaseController {

    @RequestMapping(method = RequestMethod.GET, path = "/")
    public String index() {
        return "home";
    }

    @GetMapping("/greet")
    public String indexWithParam(@RequestParam("name")String name, Model model) {
        model.addAttribute("name", name);
        return "home";
    }

    @GetMapping("/greet/{name}")
    public String indexWithPathVariable(@PathVariable("name")String name, Model model) {
        model.addAttribute("name", name);
        return "home";
    }

}
```

Anotasi `@Controller` berfungsi untuk menandakan sebuah kelas sebagai controller dan akan menjadi sebuah `Bean`.
Terdapat tiga method dengan penjelasan sebagai berikut:

- Method `index`. Anotasi `@RequestMapping` berfungsi untuk memetakan web requests ke handler tertentu (dapat berupa class ataupun method). Parameter `method` pada anotasi merupakan method HTTP apa yang digunakan, sedangkan parameter `path` merupakan URL apa yang akan ditangani. Kemudian, method ini me-return sebuah halaman HTML dengan nama `home.html`.
- Method `indexWithParam`. Anotasi `@GetMapping` merupakan `@RequestMapping` yang memiliki HTTP method GET. Adapun parameter di dalamnya sama saja dengan `path` pada `RequestMapping`. Method ini memiliki dua parameter: `name` yang didapatkan menggunakan anotasi `@RequestParam` dan `model` yang pada dasarnya dapat dianggap seperti dictionary pada Python.
- Method `indexWithPathVariable`. Method ini sebenarnya mirip dengan `indexWithParam` dan hanya berbeda pada anotasi yang digunakan untuk parameter `name`.
- Method kedua digunakan untuk menangani URL dalam bentuk `/greet?name=sebuahInputNama`. Sedangkan method ketiga digunakan untuk menangani URL dalam bentuk `/greet/sebuahInputNama`.

## Templates

Setelah mengimplementasi controller, kita lanjutkan membuat templates HTML.

`home.html`

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
  <head>
    <meta charset="UTF-8" />
    <title>Home</title>
  </head>
  <body>
    <h3 th:if="${name != null}" th:text="${'Welcome home, ' + name}"></h3>
    <h3 th:unless="${name != null}">Welcome</h3>
  </body>
</html>
```

---

# Weekly Activity Recorder

> Author: `AUL`

Setelah memahami dasar kerja Spring Boot, kamu akan mengimplementasi pengetahuan tersebut melalui sebuah aplikasi pencatat aktivitas mingguan sederhana. Aplikasi ini pada dasarnya memungkinkan kamu untuk membuat `Activity` baru dan menampilkannya di halaman lain. Ini bukan aplikasi baru, namun kamu akan membuatnya menjadi lebih baik.

## Model

Pertama-tama, kita akan membuat `model` yang akan digunakan pada aplikasi ini.

`Activity.java`

```java
package id.ac.ui.cs.advprog.tutorial0.model;

import lombok.Getter;
import lombok.Setter;

@Getter @Setter
public class Activity {
    private String name;
    private Day day;
}
```

`Day.java`

```java
package id.ac.ui.cs.advprog.tutorial0.model;

public enum Day {
    SUNDAY,
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY
}
```

Anotasi `@Getter` dan `@Setter` dari `Lombok` akan men-generate default getter/setter secara otomatis, sehingga kamu tidak perlu menuliskannya secara eksplisit. Kemudian, `enum` merupakan kelas khusus pada Java yang merepresentasikan sekelompok konstanta.

### Repository

Setelah selesai membuat model, kita perlu membuat sebuah `repository`.

`ActivityRepository.java`

```java
package id.ac.ui.cs.advprog.tutorial0.repository;

import id.ac.ui.cs.advprog.tutorial0.model.Activity;
import org.springframework.stereotype.Repository;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

@Repository
public class ActivityRepository {

    private List<Activity> activityInMemory = new ArrayList<>();

    public Activity create(Activity activity) {
        activityInMemory.add(activity);
        return activity;
    }

    public Iterator<Activity> findAll() {
        return activityInMemory.iterator();
    }

}
```

Repository ini hanya basis data sederhana yang kita buat menggunakan struktur data biasa. Kita belum menggunakan repository yang terhubung langsung ke basis data dari Spring Boot. Anotasi `@Repository` memiliki peran mirip dengan `@Controller`.

## Service

Selanjutnya kita membuat `service`. Kita membuat sebuah interface dan sebuah kelas yang mengimplementasi interface tersebut.

`ActivityService.java`

```java
package id.ac.ui.cs.advprog.tutorial0.service;

import id.ac.ui.cs.advprog.tutorial0.model.Activity;
import id.ac.ui.cs.advprog.tutorial0.model.Day;

import java.util.List;

public interface ActivityService {
    public Activity create(Activity activity);
    public List<Activity> findAll();
}
```

`ActivityServiceImpl.java`

```java
package id.ac.ui.cs.advprog.tutorial0.service;

import id.ac.ui.cs.advprog.tutorial0.model.Activity;
import id.ac.ui.cs.advprog.tutorial0.model.Day;
import id.ac.ui.cs.advprog.tutorial0.repository.ActivityRepository;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;
import java.util.stream.Collectors;

@Service
public class ActivityServiceImpl implements ActivityService {

    @Autowired
    private ActivityRepository activityRepository;

    @Override
    public Activity create(Activity activity) {
        activityRepository.create(activity);
        return activity;
    }

    @Override
    public List<Activity> findAll() {
        Iterator<Activity> activityIterator = activityRepository.findAll();
        List<Activity> allActivity = new ArrayList<>();
        activityIterator.forEachRemaining(allActivity::add);
        return allActivity;
    }

}
```

Anotasi `@Service` memiliki peran mirip dengan `@Repository`. Sedangkan anotasi `@Autowired` merupakan sebuah mekanisme dependency injection. Kita tidak melakukan inisialisasi `ActivityRepository` secara eksplisit karena fitur autowiring tersebut.

## Controller

Setelah selesai mengimplementasi service, kita sudah dapat menggunakannya untuk `controller`.

`ActivityController.java`

```java
package id.ac.ui.cs.advprog.tutorial0.controller;

import id.ac.ui.cs.advprog.tutorial0.model.Activity;
import id.ac.ui.cs.advprog.tutorial0.model.Day;
import id.ac.ui.cs.advprog.tutorial0.service.ActivityService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@Controller
@RequestMapping("/activity")
public class ActivityController {

    @Autowired
    private ActivityService service;

    @GetMapping("/list")
    public String activityListPage(Model model) {
        List<Activity> allActivities = service.findAll();
        model.addAttribute("activities", allActivities);
        return "activityList";
    }

    @GetMapping("/create")
    public String createActivityPage(Model model) {
        Activity activity = new Activity();
        model.addAttribute("activity", activity);
        return "createActivity";
    }

    @PostMapping("/create")
    public String createActivityPost(@ModelAttribute Activity activity, Model model) {
        service.create(activity);
        return "redirect:list";
    }

}
```

Ini adalah contoh controller yang menangani pembuatan `Activity` baru dan menampilkan seluruh daftar `Activity` yang ada. Proses pembuatan `Activity` terbagi menjadi dua: `createActivityPage`akan mengarahkan pada form untuk membuat `Activity` serta `createActivityPost` akan meng-submit form tersebut ke backend. Adapun string yang di-return method tersebut merupakan nama file HTML yang akan ditampilkan di frontend.

## Templates

Langkah terakhir, kita perlu membuat file HTML yang dikembalikan oleh controller.

`activityList.html`

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
  <head>
    <meta charset="UTF-8" />
    <title>Activity List</title>
    <link
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <div class="container my-2">
      <h2>Activity' List</h2>
      <a th:href="@{/activity/create}" class="btn btn-primary btn-sm mb-3"
        >Create Activity</a
      >

      <table border="1" class="table table-striped table-responsive-md">
        <thead>
          <tr>
            <th scope="col">Activity Name</th>
            <th scope="col">Day</th>
          </tr>
        </thead>
        <tbody>
          <tr th:each="activity: ${activities}">
            <td th:text="${activity.name}"></td>
            <td th:text="${activity.day}"></td>
          </tr>
        </tbody>
      </table>
    </div>

    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p"
      crossorigin="anonymous"
    ></script>
  </body>
</html>
```

`createActivity.html`

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
  <head>
    <meta charset="UTF-8" />
    <title>Create New Activity</title>
    <link
      href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <div class="container">
      <h3>Create New Activity</h3>

      <form
        th:action="@{/activity/create}"
        th:object="${activity}"
        method="post"
      >
        <div class="form-group">
          <label for="nameInput">Name</label>
          <input
            th:field="*{name}"
            type="text"
            class="form-control mb-4 col-4"
            id="nameInput"
            placeholder="Enter activity' name"
          />
        </div>
        <div class="form-group">
          <label for="dayInput">Day</label>
          <select
            class="form-control selectpicker mb-4 col-4"
            th:field="*{day}"
            id="dayInput"
          >
            <option value="">Nothing selected</option>
            <option
              th:each="day : ${T(id.ac.ui.cs.advprog.tutorial0.model.Day).values()}"
              th:value="${day}"
              th:text="${day}"
            >
              day
            </option>
          </select>
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>
    </div>

    <script
      src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js"
      integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p"
      crossorigin="anonymous"
    ></script>
  </body>
</html>
```

Setelah berhasil memahami fitur dasar pada aplikasi ini, kamu diminta mengimplementasikan satu fitur tambahan agar aplikasi dapat menampilkan daftar `Activity` untuk hari tertentu. Untuk membantu pengerjaan, silakan tambahkan kode berikut.

`ActivityService.java`

```java
public interface ActivityService {
    // ...
    public List<Activity> findByDay(Day day);
}
```

`ActivityServiceImpl.java`

```java
public class ActivityServiceImpl implements ActivityService {
    // ...
    @Override
    public List<Activity> findByDay(Day day) {
        // TO DO: get a list of activities that match the day
        return null;
    }
}
```

`ActivityController.java`

```java
public class ActivityController {
    // ...
    @GetMapping("/list/{day}")
    public String indexWithPathVariable(@PathVariable("day") String day, Model model) {
        Day dayEnum = Day.valueOf(Day.class, day.toUpperCase());
        // TO DO: call the appropriate service and send the returned value to the HTML file
        return null;
    }
}
```

## Requirements

- Menampilkan `Activity` untuk hari tertentu
  - Diakses melalui endpoint: `/activity/list/{day}`
  - Parameter day bersifat case-insensitive. Sebagai contoh, `/activity/list/FRIDAY` dan `/activity/list/frIDaY` sama-sama berlaku dan menampilkan seluruh `Activity` pada hari Jumat (Friday).

</div>
