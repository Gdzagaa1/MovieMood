## MovieMood

MovieMood is our team-built movie diary, inspired by Letterboxd. It is a Java EE full-stack web app where friends can save movies, talk about them and see what everyone is watching in real time.

### What it does
- Sign up with email (verification code) or Google Sign-In.
- Keep a personal watchlist, favorites, ratings and written reviews.
- Build custom lists (public or private) and drop movies into them quickly.
- Send and accept friend requests, then follow a shared activity feed.
- Open movie detail pages powered by TMDB posters, backdrops and metadata.

### How it works
- Java 11 + Maven build a WAR for any Servlet 4 container (Tomcat 9+).
- JSP views plus servlets handle pages like login, profile, lists and watchlist.
- Front end is plain HTML/CSS with vanilla JavaScript modules for sliders, pagination, auth widgets and movie detail interactions.
- DAOs talk to MySQL; Apache Commons DBCP2 manages pooled connections.
- OkHttp + Gson fetch movie data from TMDB.
- BCrypt hashes passwords, Jakarta Mail sends verification codes, MockWebServer and Mockito cover tests.

### Tech & languages at a glance
- **Backend:** Java Servlets/JSP, JDBC DAOs, Jakarta Mail, BCrypt, Apache Commons DBCP2.
- **Frontend:** JSP templates rendered to HTML, custom CSS, vanilla JavaScript for UI behavior.
- **APIs & data:** TMDB REST API via OkHttp + Gson, MySQL 8 for persistence, H2 for tests.
- **Tooling:** Maven for builds, Tomcat for deployment, JUnit/Mockito/MockWebServer for testing.

---

## Quick Start
1. **Install** Java 11, Maven 3.9+ and MySQL 8 locally.
2. **Clone & build**
3. **Database**: create a schema named `moviemoodDB` and grant a user.
4. **Config**: update `src/main/resources/application.properties` with your DB creds, TMDB API key and image URLs. Replace the Gmail password inside `EmailService` and the Google OAuth client ID inside `GoogleAuthServlet` with real values (ideally load them from env vars).
5. **Deploy**: copy `target/moviemood.war` to Tomcat’s `webapps/` and browse `http://localhost:8080/moviemood`.

Startup runs `DatabaseInitListener`, which creates tables (users, friend requests, watchlist, favorites, lists, ratings, reviews) and the `friends_activity_view`. No manual SQL migration is required for a blank schema.

---

## Testing
- Uses H2 in-memory DB plus schema helpers from `TestDatabaseHelper`.
- MockWebServer covers TMDB calls; Mockito stubs DAOs/services as needed.
- `-Dtest.mode=true` keeps the email service in dry-run mode.

---

## Project layout
```
MovieMood/
├─ pom.xml
├─ src/main/java/com/moviemood/
│  ├─ bean/        (User, Movie, FriendActivity, etc.)
│  ├─ dao/         (UserDao, WatchlistDao, RatingsDao…)
│  ├─ repository/  (TMDB + API clients)
│  ├─ services/    (EmailService, helpers)
│  └─ servlets/    (Login, Register, Lists, Watchlist, Reviews…)
├─ src/main/webapp/ (JSP pages, CSS, JS, WEB-INF)
├─ src/test/java/   (DAO + service tests)
└─ README.md
```

---

## Team note
Every part of MovieMood from the JSP screens to the DAO queries was built by our team. We split tasks, reviewed each other’s code and shaped the product together so it feels like our own take on Letterboxd.
