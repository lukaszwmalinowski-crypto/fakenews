<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Dezinformacja w praktyce urzędu - interaktywny panel</title>
  <style>
    :root{
      --bg:#f7f4ef;--card:#fffdf9;--ink:#1d1d1f;--muted:#68625d;--brand:#e95f54;--brand2:#ffb6aa;--line:#eadfd6;--ok:#147a43;--bad:#a82922;--soft:#fff1ee;--blue:#263e73;
    }
    *{box-sizing:border-box} html{scroll-behavior:smooth} body{margin:0;font-family:Inter,Segoe UI,Roboto,Arial,sans-serif;background:linear-gradient(180deg,#fff8f5 0%,var(--bg) 48%,#fff 100%);color:var(--ink);line-height:1.55}
    header{position:relative;overflow:hidden;padding:54px 22px 38px;border-bottom:1px solid var(--line);background:radial-gradient(circle at top right,#ffc5bd 0,#ffc5bd 18%,transparent 19%),linear-gradient(135deg,#fff 0,#fff3f0 100%)}
    .wrap{max-width:1180px;margin:0 auto}.eyebrow{display:inline-flex;gap:8px;align-items:center;background:#111;color:#fff;border-radius:999px;padding:7px 13px;font-size:13px;font-weight:800;letter-spacing:.04em;text-transform:uppercase}.hero{display:grid;grid-template-columns:1.2fr .8fr;gap:28px;align-items:center}.hero h1{font-size:clamp(34px,5vw,66px);line-height:.98;margin:18px 0 16px;letter-spacing:-.05em}.hero p{font-size:20px;color:#38312e;max-width:760px}.hero-card{background:var(--card);border:1px solid var(--line);border-radius:28px;padding:24px;box-shadow:0 24px 80px rgba(85,49,40,.12)}
    .quick{display:grid;grid-template-columns:repeat(4,1fr);gap:12px;margin-top:28px}.quick a,.btn{border:1px solid var(--line);background:#fff;border-radius:16px;padding:13px 15px;text-decoration:none;color:var(--ink);font-weight:800;display:flex;align-items:center;justify-content:space-between;gap:10px;cursor:pointer}.quick a:hover,.btn:hover{border-color:var(--brand);box-shadow:0 8px 24px rgba(233,95,84,.16)}
    main{padding:34px 20px}.section{max-width:1180px;margin:0 auto 24px;background:var(--card);border:1px solid var(--line);border-radius:28px;padding:26px;box-shadow:0 12px 40px rgba(50,35,28,.06)}
    .section h2{font-size:clamp(26px,3vw,40px);line-height:1.08;letter-spacing:-.035em;margin:0 0 10px}.section h3{font-size:22px;margin:24px 0 8px}.lead{font-size:18px;color:#48403b}.pill{display:inline-block;background:var(--soft);color:#8b2b23;padding:6px 10px;border-radius:999px;font-weight:800;font-size:13px;margin:3px 4px 3px 0}.grid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:18px}.grid3{display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:16px}.card{background:#fff;border:1px solid var(--line);border-radius:22px;padding:18px}.card strong{color:#111}.note{background:#fff9e8;border:1px solid #f0dfaa;border-radius:18px;padding:15px;color:#51442a}.source{font-size:12px;color:var(--muted);margin-top:8px}.imgcard{padding:0;overflow:hidden}.imgcard img{width:100%;display:block;background:#eee}.imgcap{padding:12px 14px;font-size:13px;color:var(--muted)}
    .gallery{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:12px}.example{background:#fff;border:1px solid var(--line);border-radius:18px;overflow:hidden}.example img{width:100%;aspect-ratio:4/3;object-fit:cover;display:block}.example div{padding:12px}.example h4{margin:0 0 4px;font-size:16px}.example p{margin:0;color:var(--muted);font-size:13px}.clickable{cursor:pointer}.modal{display:none;position:fixed;z-index:99;inset:0;background:rgba(0,0,0,.75);align-items:center;justify-content:center;padding:24px}.modal.open{display:flex}.modal img{max-width:min(1100px,96vw);max-height:90vh;background:white;border-radius:12px}.modal button{position:absolute;top:18px;right:18px;background:#fff;border:0;border-radius:999px;padding:10px 14px;font-weight:800;cursor:pointer}
    details{border:1px solid var(--line);background:#fff;border-radius:18px;padding:14px 16px;margin:12px 0}summary{font-weight:900;cursor:pointer}.task{border-left:5px solid var(--brand);background:#fff7f5;border-radius:16px;padding:16px;margin:14px 0}.task label{display:block;font-weight:800;margin-bottom:8px}.task textarea,.task input{width:100%;min-height:78px;border:1px solid var(--line);border-radius:14px;padding:12px;font:inherit;background:#fff}.task input{min-height:auto}.row{display:flex;gap:10px;flex-wrap:wrap}.mini{font-size:13px;color:var(--muted)}
    .checklist label{display:flex;gap:10px;align-items:flex-start;margin:9px 0;background:#fff;border:1px solid var(--line);border-radius:14px;padding:10px}.checklist input{margin-top:5px}.tabs{display:flex;gap:8px;flex-wrap:wrap;margin:14px 0}.tab{border:1px solid var(--line);border-radius:999px;background:#fff;padding:9px 13px;font-weight:800;cursor:pointer}.tab.active{background:#111;color:#fff}.panel{display:none}.panel.active{display:block}.test-box{background:#111;color:#fff;border-radius:24px;padding:22px;margin-top:18px}.question{background:#fff;color:#111;border-radius:18px;padding:18px;margin:14px 0;border:2px solid transparent}.question.answered{border-color:#ddd}.question h4{margin:0 0 10px}.answers label{display:block;border:1px solid var(--line);border-radius:14px;padding:10px 12px;margin:8px 0;cursor:pointer;background:#fff}.answers input{margin-right:8px}.result{display:none;margin-top:18px;background:#fff;color:#111;border-radius:20px;padding:20px}.score{font-size:40px;font-weight:950;letter-spacing:-.04em}.good{color:var(--ok)}.wrong{color:var(--bad)}.feedback{border-top:1px solid var(--line);padding-top:12px;margin-top:12px}.toolbar{position:sticky;bottom:12px;z-index:20;max-width:1180px;margin:0 auto 18px;display:flex;justify-content:center;gap:10px;pointer-events:none}.toolbar button{pointer-events:auto}.btn.primary{background:#111;color:#fff}.btn.danger{background:var(--brand);color:#fff;border-color:var(--brand)}
    footer{padding:24px 20px 50px;color:var(--muted);text-align:center}.badge{display:inline-grid;place-items:center;width:34px;height:34px;border-radius:12px;background:#111;color:#fff;font-weight:900;margin-right:8px}.scenario{background:#f4f7ff;border:1px solid #dce5ff;border-radius:18px;padding:16px}.print-only{display:none}
    @media(max-width:900px){.hero{grid-template-columns:1fr}.quick{grid-template-columns:1fr 1fr}.grid,.grid3{grid-template-columns:1fr}.gallery{grid-template-columns:1fr 1fr}.section{padding:20px}.toolbar{position:static;flex-wrap:wrap}}
    @media print{header,.quick,.toolbar,.btn,.tabs,.modal{display:none!important}.section{box-shadow:none;page-break-inside:avoid}.panel{display:block!important}.print-only{display:block}.question{break-inside:avoid}body{background:white}}
  </style>
</head>
<body>
  <header>
    <div class="wrap hero">
      <div>
        <span class="eyebrow">Fake? Fake! - wersja dla urzędów</span>
        <h1>Dezinformacja w praktyce urzędu</h1>
        <p>Interaktywny panel szkoleniowy dla dorosłych uczestników: pracowników urzędów, instytucji publicznych i osób odpowiedzialnych za komunikację z mieszkańcami.</p>
        <div class="quick">
          <a href="#moduly">Moduły <span>↓</span></a>
          <a href="#galeria">Przykłady ze zdjęciami <span>↓</span></a>
          <a href="#test">Test z wynikiem <span>↓</span></a>
          <a href="#notatki">Notatki <span>↓</span></a>
        </div>
      </div>
      <div class="hero-card">
        <h3>Cel szkolenia</h3>
        <p class="lead">Po szkoleniu uczestnik potrafi rozpoznać ryzykowną treść, ocenić źródło, odróżnić fakt od opinii, zauważyć manipulację i dobrać rozsądną reakcję w kontekście pracy urzędu.</p>
        <span class="pill">fake news</span><span class="pill">boty i trolle</span><span class="pill">lateral reading</span><span class="pill">fakt vs opinia</span><span class="pill">manipulacja</span><span class="pill">dieta medialna</span>
      </div>
    </div>
  </header>

  <main>
    <section class="section" id="moduly">
      <h2>1. Mapa szkolenia</h2>
      <p class="lead">Materiał został przerobiony z krótkich scenariuszy lekcyjnych na praktyczny warsztat dla dorosłych. Zamiast sytuacji szkolnych są tu decyzje urzędowe: komunikat na stronie, komentarz pod postem, rozmowa z mieszkańcem, weryfikacja źródła i wybór kanałów informacji.</p>
      <div class="grid3">
        <div class="card"><span class="badge">1</span><strong>Rozpoznaj</strong><br>Co jest informacją fałszywą, a co tylko opinią lub żartem?</div>
        <div class="card"><span class="badge">2</span><strong>Sprawdź</strong><br>Kto publikuje treść, czy inne źródła ją potwierdzają i jaki jest kontekst?</div>
        <div class="card"><span class="badge">3</span><strong>Zareaguj</strong><br>Czy odpowiadać publicznie, zgłosić, skonsultować, czy zostawić bez reakcji?</div>
      </div>
      <div class="task" id="notatki">
        <label>Twoje pierwsze skojarzenia z dezinformacją w pracy urzędu</label>
        <textarea data-save="intro" placeholder="Np. fałszywy post o świadczeniach, plotka o naborze, zmanipulowany screen pisma, agresywne komentarze pod profilem urzędu..."></textarea>
      </div>
    </section>

    <section class="section" id="galeria">
      <h2>2. Przykłady ze zdjęciami z prezentacji</h2>
      <p class="lead">Kliknij kartę, żeby powiększyć obraz. Każdy przykład można omówić pytaniem: „Co tu wygląda podejrzanie?” oraz „Jaka byłaby bezpieczna reakcja urzędu?”.</p>
      <div class="gallery">
        <div class="example clickable"><img src="assets/crop_sfabrykowana.jpg" alt="Sfabrykowana informacja"><div><h4>Sfabrykowana informacja</h4><p>Treść zmyślona, udająca fakt.</p></div></div>
        <div class="example clickable"><img src="assets/crop_zmanipulowana.jpg" alt="Treść zmanipulowana"><div><h4>Treść zmanipulowana</h4><p>Prawdziwy element przerobiony lub pokazany fałszywie.</p></div></div>
        <div class="example clickable"><img src="assets/crop_podszywanie.jpg" alt="Podszywanie się"><div><h4>Podszywanie się</h4><p>Konto lub profil udaje znaną instytucję albo firmę.</p></div></div>
        <div class="example clickable"><img src="assets/crop_falszywy_kontekst.jpg" alt="Fałszywy kontekst"><div><h4>Fałszywy kontekst</h4><p>Obraz prawdziwy, ale opis wprowadza w błąd.</p></div></div>
        <div class="example clickable"><img src="assets/crop_wprowadzajace_w_blad.jpg" alt="Treść wprowadzająca w błąd"><div><h4>Wprowadzenie w błąd</h4><p>Pomija się ważny fragment informacji.</p></div></div>
        <div class="example clickable"><img src="assets/crop_falszywy_zwiazek.jpg" alt="Fałszywy związek"><div><h4>Fałszywy związek</h4><p>Nagłówek, opis albo zdjęcie nie pasują do siebie.</p></div></div>
        <div class="example clickable"><img src="assets/crop_satyra.jpg" alt="Satyra i parodia"><div><h4>Satyra/parodia</h4><p>Żart może zostać odebrany jako fakt albo użyty do manipulacji.</p></div></div>
        <div class="example clickable"><img src="assets/przyklady_7_typow.jpg" alt="Pełna strona przykładów"><div><h4>Pełna plansza</h4><p>Cały zestaw przykładów z materiału źródłowego.</p></div></div>
      </div>
      <p class="source">Źródło grafik: materiał szkoleniowy „Fake? Fake!”, opracowany przez Stowarzyszenie Demagog i partnerów projektu. Wykorzystanie w panelu: niekomercyjny materiał edukacyjny.</p>
      <div class="task">
        <label>Zadanie: wybierz jeden przykład z galerii i opisz ryzyko dla urzędu</label>
        <textarea data-save="galeria" placeholder="Jaki typ fałszywej informacji widzisz? Jakie emocje może wywołać? Co powinien zrobić pracownik urzędu?"></textarea>
      </div>
    </section>

    <section class="section">
      <h2>3. Boty, trolle i komentarze pod profilami publicznymi</h2>
      <div class="grid">
        <div>
          <p class="lead">W pracy urzędu komentarz w internecie nie zawsze oznacza autentyczną opinię mieszkańca. Część wpisów może pochodzić z kont automatycznych, fałszywych lub celowo prowokacyjnych.</p>
          <div class="checklist">
            <label><input type="checkbox"> Konto nie ma zdjęcia, historii aktywności albo obserwujących.</label>
            <label><input type="checkbox"> Komentarz jest skrajnie emocjonalny i dzieli ludzi na „my” i „oni”.</label>
            <label><input type="checkbox"> Ten sam przekaz pojawia się masowo w wielu miejscach.</label>
            <label><input type="checkbox"> Język wygląda jak automatyczne tłumaczenie lub gotowy szablon.</label>
          </div>
        </div>
        <div class="card imgcard clickable"><img src="assets/bot_troll_komentarze.jpg" alt="Boty, trolle i komentarze"><div class="imgcap">Plansza z komentarzem, profilem i infografiką o botach oraz trollach.</div></div>
      </div>
      <details><summary>Procedura dla pracownika urzędu</summary><p>Nie karm trolla. Nie odpowiadaj w emocjach. Zrób zrzut ekranu, sprawdź profil, oceń ryzyko, skonsultuj odpowiedź z osobą odpowiedzialną za komunikację. Jeżeli wpis zawiera groźby, dane osobowe lub mowę nienawiści - zgłoś zgodnie z procedurą.</p></details>
      <div class="task"><label>Ćwiczenie: czerwona i biała flaga</label><textarea data-save="boty" placeholder="Wypisz 2 czerwone flagi podejrzanego komentarza i 2 dobre praktyki odpowiadania jako urząd."></textarea></div>
    </section>

    <section class="section">
      <h2>4. Wiarygodność źródła - sprawdzanie w poziomie</h2>
      <div class="grid">
        <div class="card imgcard clickable"><img src="assets/sprawdzanie_w_poziomie.jpg" alt="Sprawdzanie w poziomie"><div class="imgcap">Infografika o metodzie lateral reading - sprawdzaniu źródła poza samą stroną.</div></div>
        <div>
          <p class="lead">Zanim wejdziesz głęboko w treść artykułu, sprawdź, kto ją publikuje i co mówią o tym źródle inne strony.</p>
          <div class="card"><strong>5 pytań kontrolnych:</strong><br>1. Kto jest autorem lub właścicielem strony?<br>2. Czy jest kontakt, redakcja, regulamin?<br>3. Czy inne wiarygodne źródła potwierdzają informację?<br>4. Czy tekst nie ukrywa ważnego kontekstu?<br>5. Kto może zyskać na takim przekazie?</div>
          <div class="task"><label>Sprawdź źródło</label><input data-save="zrodlo" placeholder="Wklej adres strony lub nazwę profilu do sprawdzenia"><textarea data-save="zrodlo_wynik" placeholder="Co udało się ustalić o źródle?"></textarea></div>
        </div>
      </div>
    </section>

    <section class="section">
      <h2>5. Fakt, opinia, prawda i fałsz</h2>
      <div class="grid">
        <div><p class="lead">W urzędzie szczególnie ważne jest oddzielanie informacji od komentarza. Fakt można sprawdzić. Opinia pokazuje ocenę, wrażenie lub stanowisko.</p>
          <div class="scenario"><strong>Przykład urzędowy:</strong><br>„Nabór wniosków trwa do 30 czerwca” - fakt.<br>„Ten nabór jest wyjątkowo trudny” - opinia.<br>„Urząd celowo utrudnia dostęp do środków” - mocna teza wymagająca dowodów.</div>
        </div>
        <div class="card imgcard clickable"><img src="assets/fakt_opinia.jpg" alt="Fakt czy opinia"><div class="imgcap">Plansza z materiału: ćwiczenie odróżniania faktu od opinii.</div></div>
      </div>
      <div class="task"><label>Zadanie: przerób zdanie emocjonalne na neutralny komunikat urzędowy</label><textarea data-save="fakt_opinia" placeholder="Wpisz przykład zdania i jego neutralną wersję."></textarea></div>
    </section>

    <section class="section">
      <h2>6. Techniki manipulacji i manipulacja językowa</h2>
      <p class="lead">Materiał źródłowy wyróżnia m.in. emocjonalny język, niespójność, fałszywą dychotomię, kozła ofiarnego i ataki ad personam. W urzędzie te techniki mogą pojawić się pod postami, w mailach, w telefonach od mieszkańców lub w lokalnych grupach.</p>
      <div class="grid">
        <div class="card imgcard clickable"><img src="assets/techniki_manipulacji.jpg" alt="Techniki manipulacji"><div class="imgcap">Karta pracy z technikami manipulacji.</div></div>
        <div class="card imgcard clickable"><img src="assets/manipulacja_jezykowa_screeny.jpg" alt="Screeny manipulacji językowej"><div class="imgcap">Przykładowe screeny do analizy języka i emocji.</div></div>
      </div>
      <div class="grid3">
        <div class="card"><strong>Emocjonalny język</strong><br>Strach, oburzenie, wielkie litery, wykrzykniki.</div>
        <div class="card"><strong>Fałszywa dychotomia</strong><br>Udawanie, że są tylko dwie możliwości.</div>
        <div class="card"><strong>Ad personam</strong><br>Atak na osobę zamiast na argument.</div>
      </div>
      <div class="task"><label>Ćwiczenie: zaznacz manipulację</label><textarea data-save="manipulacja" placeholder="Wymyśl lub wklej zdanie z komentarza. Jaką technikę widzisz? Jak można odpowiedzieć rzeczowo?"></textarea></div>
    </section>

    <section class="section">
      <h2>7. Krytyczne wyszukiwanie informacji</h2>
      <div class="grid">
        <div>
          <p class="lead">Samo wpisanie hasła w wyszukiwarkę to za mało. Pracownik urzędu powinien umieć szukać precyzyjnie: w konkretnym serwisie, po dokładnej frazie, z pominięciem niechcianych wyników.</p>
          <div class="card"><strong>Przydatne operatory:</strong><br><code>"dokładna fraza"</code> - szuka dokładnego cytatu<br><code>site:gov.pl świadczenie</code> - szuka w obrębie domeny<br><code>-plotka</code> - wyklucza słowo<br><code>filetype:pdf</code> - szuka PDF</div>
        </div>
        <div class="card imgcard clickable"><img src="assets/operatory_wyszukiwania.jpg" alt="Operatory wyszukiwania"><div class="imgcap">Infografika o operatorach wyszukiwania.</div></div>
      </div>
      <div class="task"><label>Zadanie: zapisz zapytanie do wyszukiwarki</label><textarea data-save="wyszukiwanie" placeholder="Np. site:katowice.praca.gov.pl \"nabór\" filetype:pdf"></textarea></div>
    </section>

    <section class="section">
      <h2>8. Dieta medialna pracownika instytucji publicznej</h2>
      <div class="grid">
        <div class="card imgcard clickable"><img src="assets/dieta_medialna.jpg" alt="Dieta medialna"><div class="imgcap">Karta „Moja dieta medialna” - monitoring źródeł informacji.</div></div>
        <div>
          <p class="lead">Dieta medialna to nie zakaz korzystania z social mediów. To świadomy dobór źródeł, tak aby nie żyć tylko w bańce informacyjnej i nie opierać decyzji na przypadkowych postach.</p>
          <div class="task"><label>Moje źródła informacji</label><textarea data-save="dieta1" placeholder="Z jakich źródeł korzystam przynajmniej raz w tygodniu?"></textarea></div>
          <div class="task"><label>Co ograniczam, co dodaję?</label><textarea data-save="dieta2" placeholder="Których źródeł jest za dużo? Jakie wiarygodne źródła dodam?"></textarea></div>
        </div>
      </div>
    </section>

    <section class="section" id="test">
      <h2>9. Test końcowy z automatycznym wynikiem</h2>
      <p class="lead">Test ma 20 pytań. Wynik liczy się automatycznie. Próg zaliczenia możesz przyjąć np. 80% lub 90%, zależnie od szkolenia.</p>
      <div class="test-box">
        <div class="row"><button class="btn primary" onclick="gradeTest()">Sprawdź wynik</button><button class="btn" onclick="resetTest()">Wyczyść odpowiedzi</button></div>
        <div id="quiz"></div>
        <div class="result" id="result"></div>
      </div>
    </section>
  </main>

  <div class="toolbar">
    <button class="btn primary" onclick="downloadNotes()">Pobierz notatki TXT</button>
    <button class="btn" onclick="window.print()">Drukuj / zapisz PDF</button>
    <button class="btn danger" onclick="localStorage.clear(); location.reload()">Wyczyść wszystko</button>
  </div>
  <div class="modal" id="modal" onclick="closeModal()"><button>Zamknij ×</button><img id="modalImg" alt="Powiększony obraz"></div>
  <footer>Panel szkoleniowy - wersja robocza do wykorzystania wewnętrznego i niekomercyjnego. Grafiki pochodzą z materiału źródłowego przekazanego do opracowania.</footer>

<script>
const questions = [
 {q:'Fałszywa informacja przedstawiana jako fakt, ale niezgodna z prawdą, to:', a:['opinia','fałszywa informacja','komentarz ekspercki','sprostowanie'], ok:1, why:'Fałszywa informacja udaje fakt, choć nie jest zgodna z rzeczywistością.'},
 {q:'Dezinformacja różni się tym, że zwykle jest rozpowszechniana:', a:['z intencją wyrządzenia szkody lub osiągnięcia wpływu','wyłącznie jako żart','tylko przez media tradycyjne','zawsze przez przypadek'], ok:0, why:'Kluczowa jest intencja: wpływ, szkoda, zysk, rozgłos lub manipulacja.'},
 {q:'Profil bez zdjęć, historii aktywności i obserwujących może wskazywać na:', a:['źródło pierwotne','bota lub fałszywe konto','oficjalny profil urzędu','portal naukowy'], ok:1, why:'To jedna z czerwonych flag przy ocenie komentarzy.'},
 {q:'Najbezpieczniejsza reakcja na skrajnie prowokacyjny komentarz pod profilem urzędu to:', a:['natychmiastowa emocjonalna odpowiedź','udostępnienie komentarza dalej','ocena ryzyka, screen, ewentualna konsultacja i rzeczowa reakcja','atak na autora komentarza'], ok:2, why:'Urząd powinien działać spokojnie, proceduralnie i rzeczowo.'},
 {q:'Sprawdzanie w poziomie oznacza:', a:['czytanie tylko jednego artykułu do końca','ocenę źródła przez sprawdzenie go w innych miejscach','sprawdzanie literówek','przewijanie strony poziomo'], ok:1, why:'Lateral reading polega na sprawdzeniu źródła poza samą badaną stroną.'},
 {q:'Które pytanie najlepiej pomaga ocenić źródło?', a:['Czy zgadzam się z tekstem?','Czy autor używa ładnej grafiki?','Kto jest właścicielem strony i czy inne źródła ją potwierdzają?','Czy tytuł jest emocjonalny?'], ok:2, why:'Wiarygodność nie polega na zgodności z naszym poglądem, tylko na możliwości weryfikacji.'},
 {q:'Zdanie „Nabór trwa do 30 czerwca” to najczęściej:', a:['fakt możliwy do sprawdzenia','opinia','satyra','atak personalny'], ok:0, why:'Ma konkretną treść, którą można zweryfikować w dokumentach lub komunikacie.'},
 {q:'Zdanie „Ten nabór jest wyjątkowo trudny” to:', a:['fakt urzędowy','opinia lub ocena','dokument źródłowy','bot'], ok:1, why:'Zawiera ocenę, nie samą informację o faktach.'},
 {q:'Prawdziwe zdjęcie opisane jako aktualne, choć pochodzi sprzed kilku lat, to:', a:['podszywanie się','fałszywy kontekst','fakt','źródło pierwotne'], ok:1, why:'Obraz może być prawdziwy, ale kontekst fałszywy.'},
 {q:'Konto udające znaną firmę i obiecujące darmowe nagrody to przykład:', a:['podszywania się','lateral reading','diety medialnej','opinii'], ok:0, why:'Fałszywy profil podszywa się pod znaną markę lub instytucję.'},
 {q:'Nagłówek lub opis niepasujący do zdjęcia to:', a:['fałszywy związek','sprawdzone źródło','fakt','cytat ekspercki'], ok:0, why:'Fałszywy związek występuje, gdy elementy przekazu sugerują coś, czego nie potwierdzają.'},
 {q:'Manipulacja językowa przez wzbudzanie strachu i oburzenia to:', a:['emocjonalny język','operator wyszukiwania','źródło pierwotne','neutralny styl'], ok:0, why:'Silne emocje mogą osłabiać krytyczną ocenę informacji.'},
 {q:'Fałszywa dychotomia polega na tym, że:', a:['pokazuje się tylko dwie opcje, choć jest ich więcej','podaje się źródło pierwotne','sprawdza się dokument PDF','oddziela się fakt od opinii'], ok:0, why:'To sztuczne zawężenie wyboru do dwóch skrajnych możliwości.'},
 {q:'Atak ad personam oznacza:', a:['sprawdzenie daty publikacji','atak na osobę zamiast odniesienia się do argumentu','cytowanie danych','porównanie kilku źródeł'], ok:1, why:'To zastąpienie argumentacji atakiem personalnym.'},
 {q:'Operator site: służy do:', a:['wyszukiwania w obrębie konkretnej strony lub domeny','usuwania komentarzy','sprawdzania grafiki','tworzenia haseł'], ok:0, why:'Np. site:gov.pl pozwala szukać wyników w domenie gov.pl.'},
 {q:'Cudzysłów w wyszukiwarce, np. "dokładna fraza", służy do:', a:['szukania dokładnego brzmienia frazy','ukrywania wyników','zgłaszania fake newsa','dodawania emocji'], ok:0, why:'Cudzysłów pomaga znaleźć konkretny cytat lub identyczny fragment tekstu.'},
 {q:'Dieta medialna oznacza:', a:['świadomy dobór źródeł informacji','brak internetu','czytanie tylko jednego portalu','komentowanie każdej sprawy'], ok:0, why:'Chodzi o higienę informacyjną i różnorodność wiarygodnych źródeł.'},
 {q:'Wiarygodne źródło to takie, które:', a:['zawsze potwierdza nasze przekonania','pozwala sprawdzić informacje i ma przejrzysty kontekst','ma najwięcej wykrzykników','publikuje anonimowo'], ok:1, why:'Źródło ma pomagać ustalać fakty, a nie tylko wzmacniać nasze emocje.'},
 {q:'Jeżeli treść wywołuje bardzo silne emocje, pracownik urzędu powinien najpierw:', a:['natychmiast ją udostępnić','zatrzymać się i sprawdzić źródło oraz kontekst','napisać złośliwy komentarz','usunąć wszystkie opinie'], ok:1, why:'Silne emocje to sygnał, że trzeba zwolnić i weryfikować.'},
 {q:'Najlepsza zasada końcowa brzmi:', a:['Szybkość jest ważniejsza niż prawda','STOP - SPRAWDŹ - ODPOWIEDZ','Nie trzeba podawać źródeł','Każdy screen jest dowodem'], ok:1, why:'Najpierw zatrzymanie, potem weryfikacja, dopiero na końcu reakcja.'}
];
function renderQuiz(){
 const box=document.getElementById('quiz');
 box.innerHTML=questions.map((it,i)=>`<div class="question" id="q${i}"><h4>${i+1}. ${it.q}</h4><div class="answers">${it.a.map((x,j)=>`<label><input type="radio" name="q${i}" value="${j}"> ${x}</label>`).join('')}</div><div class="feedback" id="f${i}" style="display:none"></div></div>`).join('');
}
function gradeTest(){
 let score=0, answered=0, html='';
 questions.forEach((it,i)=>{
   const chosen=document.querySelector(`input[name="q${i}"]:checked`);
   const fb=document.getElementById('f'+i);
   if(chosen){answered++;}
   const val=chosen?Number(chosen.value):-1;
   const ok=val===it.ok;
   if(ok) score++;
   fb.style.display='block';
   fb.innerHTML= ok ? `<strong class="good">Dobrze.</strong> ${it.why}` : `<strong class="wrong">Do poprawy.</strong> Poprawna odpowiedź: <strong>${it.a[it.ok]}</strong>. ${it.why}`;
 });
 const pct=Math.round(score/questions.length*100);
 const passed80=pct>=80, passed90=pct>=90;
 const res=document.getElementById('result');
 res.style.display='block';
 res.innerHTML=`<div class="score ${passed80?'good':'wrong'}">${score}/${questions.length} - ${pct}%</div><p>Odpowiedziano na ${answered} z ${questions.length} pytań.</p><p>${passed90?'Wynik bardzo dobry - spełnia próg 90%.':passed80?'Wynik zaliczony przy progu 80%. Do progu 90% warto poprawić pytania oznaczone jako błędne.':'Wynik poniżej 80%. Wróć do modułów i przejdź test jeszcze raz.'}</p>`;
 res.scrollIntoView({behavior:'smooth',block:'center'});
}
function resetTest(){document.querySelectorAll('input[type="radio"]').forEach(x=>x.checked=false);document.querySelectorAll('.feedback').forEach(x=>x.style.display='none');document.getElementById('result').style.display='none'}
function saveFields(){document.querySelectorAll('[data-save]').forEach(el=>{const key='panel_'+el.dataset.save; el.value=localStorage.getItem(key)||''; el.addEventListener('input',()=>localStorage.setItem(key,el.value));});}
function downloadNotes(){
 let txt='NOTATKI UCZESTNIKA - Dezinformacja w praktyce urzędu\n\n';
 document.querySelectorAll('[data-save]').forEach(el=>{txt += (el.dataset.save.toUpperCase()+':\n'+(el.value||'')+'\n\n');});
 const blob=new Blob([txt],{type:'text/plain;charset=utf-8'}); const a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='notatki_dezinformacja_urzedy.txt'; a.click(); URL.revokeObjectURL(a.href);
}
function closeModal(){document.getElementById('modal').classList.remove('open')}
function initImages(){document.querySelectorAll('.clickable img').forEach(img=>img.addEventListener('click',(e)=>{e.stopPropagation();document.getElementById('modalImg').src=img.src;document.getElementById('modal').classList.add('open')}));}
renderQuiz(); saveFields(); initImages();
</script>
</body>
</html>