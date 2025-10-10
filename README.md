<html lang="id">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>LeafCy Chat — LeafZuya</title>
<style>
  :root{
    --green1:#00c16b;
    --green2:#00994d;
    --blue1:#27a2ff;
    --bg-grad-a: #00e69a;
    --bg-grad-b: #39a7ff;
    --card: rgba(255,255,255,0.92);
    --accent: linear-gradient(135deg,var(--green1),var(--blue1));
  }
  *{box-sizing:border-box}
  html,body{height:100%; margin:0; font-family: "Poppins", "Segoe UI", Arial, sans-serif; background: linear-gradient(135deg,var(--bg-grad-a),var(--bg-grad-b));}
  .wrap{
    min-height:100vh;
    display:flex;
    align-items:center;
    justify-content:center;
    padding:28px;
  }

  .panel{
    width:960px;
    max-width:96%;
    background: linear-gradient(180deg, rgba(255,255,255,0.12), rgba(255,255,255,0.06));
    border-radius:18px;
    box-shadow: 0 18px 60px rgba(0,0,0,0.25);
    padding:18px;
    display:grid;
    grid-template-columns: 360px 1fr;
    gap:18px;
    align-items:start;
    position:relative;
    overflow:visible;
  }

  .left {
    background: var(--card);
    border-radius:14px;
    padding:14px;
    text-align:center;
    position:relative;
    min-height:440px;
    box-shadow: 0 10px 30px rgba(0,0,0,0.12);
  }

  .avatar-wrap{
    width:260px; height:260px; margin:12px auto 8px;
    border-radius:14px; overflow:hidden; display:flex; align-items:center; justify-content:center;
    background: linear-gradient(180deg,#ffffff,#f0fbff);
    box-shadow: 0 10px 20px rgba(0,0,0,0.08);
    position:relative;
  }
  .avatar-wrap img{ width:100%; height:100%; object-fit:cover; display:block; }

  .name {
    font-weight:800; color:#0a3; font-size:20px; margin-top:8px;
  }
  .subtitle { color:#467; font-size:13px; margin-top:4px; opacity:0.9; }

  .bubble {
  position:absolute;
  top:18px;
  right:-12px;
  width:280px;
  max-width:42%;
  background: linear-gradient(180deg,#fff,#f5fff9);
  border-radius:12px;
  padding:12px 14px;
  box-shadow: 0 8px 22px rgba(0,0,0,0.12);
  font-size:15px;
  color:#0a3;
  z-index:20;
  transition: transform .18s ease;
  
  /* Tambahan penting */
  max-height: 240px;         /* batas tinggi maksimal */
  overflow-y: auto;          /* biar bisa di-scroll */
  scrollbar-width: thin;     /* scrollbar tipis untuk browser modern */
  scrollbar-color: #8fe3b2 #ffffff;  /* warna scrollbar */
}

/* Scrollbar untuk Chrome, Edge, dll */
.bubble::-webkit-scrollbar {
  width: 6px;
}
.bubble::-webkit-scrollbar-thumb {
  background: linear-gradient(var(--green1), var(--blue1));
  border-radius: 6px;
}
.bubble::-webkit-scrollbar-track {
  background: transparent;
}

  .right {
    background: var(--card);
    border-radius:14px;
    padding:14px;
    min-height:440px;
    box-shadow: inset 0 2px 12px rgba(0,0,0,0.03);
  }

  .title {
    font-size:18px; font-weight:800; color: #065; display:flex; align-items:center; gap:10px;
  }
  .controls { margin-top:12px; display:flex; gap:8px; flex-wrap:wrap; align-items:center; }

  .btn {
    background: white; border:1px solid rgba(0,0,0,0.06);
    padding:10px 14px; border-radius:12px; cursor:pointer; font-weight:700;
    box-shadow: 0 6px 14px rgba(0,0,0,0.06);
  }
  .btn.primary {
    background: var(--accent); color:white; border:none;
    box-shadow: 0 10px 20px rgba(0,0,0,0.18); transform: translateY(0);
  }
  .btn:active { transform: translateY(1px) }

  .preset-list { margin-top:14px; display:flex; gap:8px; flex-wrap:wrap; }
  .preset {
    background: linear-gradient(180deg,#fff,#f4fbff);
    border-radius:10px; padding:8px 10px; cursor:pointer; border:1px solid rgba(0,0,0,0.05);
    font-weight:700; box-shadow: 0 6px 12px rgba(0,0,0,0.06);
  }

  .chat {
  margin-top:14px;
  flex: 1;                      /* biar area chat fleksibel */
  max-height: 300px;            /* tinggi maksimum chat area */
  overflow-y: auto;             /* biar bisa di-scroll */
  padding-right:6px;
  display:flex;
  flex-direction:column;
  gap:10px;
  scroll-behavior: smooth;      /* biar scroll-nya halus */
}

/* tambahkan agar bubble chat gak mengecil */
.msg {
  display: inline-block;
  width: fit-content;           /* biar gelembung menyesuaikan isi */
  max-width: 80%;               /* biar gak melebar seluruh layar */
  word-wrap: break-word;        /* potong teks panjang otomatis */
  padding:10px 12px;
  border-radius:12px;
  font-size:15px;
  box-shadow: 0 8px 18px rgba(0,0,0,0.06);
}

/* tetap kasih warna beda untuk user & LeafCy */
.msg.user {
  align-self:flex-end;
  background: linear-gradient(180deg,#e9f7ff,#e0f0ff);
  color:#024;
  border:1px solid rgba(0,0,0,0.04);
}

.msg.leafcy {
  align-self:flex-start;
  background: linear-gradient(180deg,#fffefc,#f7fff6);
  color:#063;
  border:1px solid rgba(0,0,0,0.04);
}

  .input-row { display:flex; gap:8px; margin-top:12px; align-items:center; }
  .input-row input[type="text"]{ flex:1; padding:10px;border-radius:10px;border:1px solid #ddd; font-size:15px; }
  .small-muted { font-size:12px; color:#577; margin-top:8px; }
  .foot { margin-top:12px; font-size:12px; color:#064; opacity:0.9; text-align:center; }

  @media(max-width:900px){
    .panel { grid-template-columns: 1fr; }
    .bubble { position:relative; right:auto; left:auto; margin:6px auto 0; }
  }
  /* === FOOTER BUTTON STYLE === */
.foot {
  text-align: center;
  margin-top: 20px;
}

.foot a {
  display: inline-block;
  font-size: 22px; /* 🔥 Ukuran besar dan mencolok */
  font-weight: 900;
  padding: 14px 28px;
  border-radius: 16px;
  text-decoration: none;
  color: white;
  background: linear-gradient(135deg, #ff3c00, #ffd200);
  box-shadow: 0 0 25px rgba(255, 136, 0, 0.6);
  transition: all 0.3s ease;
  margin: 8px;
  letter-spacing: 1px;
}

.foot a:hover {
  transform: scale(1.1);
  box-shadow: 0 0 40px rgba(255, 204, 0, 0.9);
  background: linear-gradient(135deg, #ff6600, #ffea00);
}
</style>
</head>
<body>
  <div class="wrap">
    <div class="panel" role="application" aria-labelledby="leafcyTitle">
      <div class="left">
        <div class="bubble" id="speechBubble">Klik tombol di kanan untuk mulai ngobrol dengan LeafCy!</div>

        <div class="avatar-wrap">
          <img id="avatarImg" src="LeafCy.jpg" alt="LeafCy avatar (GIF)">
        </div>

        <div class="name">LeafCy</div>
        <div class="subtitle">Teman Virtual — Have Fun!</div>

        <div style="margin-top:14px; display:flex; gap:8px; justify-content:center;">
          <button class="btn primary" id="btnWave">Katakan Hallo</button>
          <button class="btn" id="btnCalm">Hobimu?</button>
        </div>

        <div style="margin-top:12px; display:flex; gap:8px; justify-content:center;">
          <button class="btn" id="btnDance">Menarilah!</button>
          <button class="btn" id="btnSleep">Selamat Malam😴</button>
        </div>

        <div class="small-muted">Saat Ingin Bertanya Informasi Dengan LeafCy,Memakai <b>Kata Tanya(Apa,Siapa, Mengapa /Kenapa,Dimana,kapan,dan Bagaimana)Dan Diakhir Kalimat diberi Tanda Tanya '?'</b> agar LeafCy Dapat Mencari Informasi Dari Sumber Resmi Google
        Contohnya (Apa Ibukota Jerman?).</div>
      </div>

      <div class="right">
        <div class="title" id="leafcyTitle">Interaksi Ringan — LeafCy</div>

        <div class="controls">
          <button class="btn primary" id="btnStart">Mulai/Start</button>
          <button class="btn" id="btnClear">Clear Chat</button>
          <button class="btn" id="btnAdd">Tambahkan Obrolan Tambahan</button>
        </div>

        <div class="preset-list" id="presetList"></div>

        <div class="chat" id="chatArea"></div>

        <div class="input-row">
          <input id="textIn" type="text" placeholder="Ketik pesan (atau tekan salah satu tombol preset)..." />
          <button class="btn primary" id="btnSend">Send</button>
        </div>

        <div class="small-muted">Tip: tombol preset memberikan jawaban cepat; kamu juga bisa menambah jawaban sendiri.</div>
        <div class="foot">Made with 💚 — LeafZuya</div>
      </div>
    </div>
  </div>

<script>
const speechBubble = document.getElementById("speechBubble");
const chatArea = document.getElementById("chatArea");
const presetList = document.getElementById("presetList");
const textIn = document.getElementById("textIn");
const avatarImg = document.getElementById("avatarImg");

const RESPONSES = {
  "Halo": ["Halo juga! Aku LeafCy 😎, gimana kabarnya?", "Hai! Senang ketemu kamu lagi!"],
  "Kenapa Namamu LeafCy?": ["LeafCy,Adalah Nama Kreativitas Dari Leafzuya.....Leafzuya pertama kali menemukan nama ini,saat Dia Sedang Buang Air Besar(BAB) di Kamar mandinya"],
  "Siapa kamu?": ["Aku LeafCy — asisten dan teman virtualmu! 🍃", "Namaku LeafCy, si pembuat suasana fun dan hijau~"],
  "Menurutmu,Siapa Itu Bahlil Raja Ampat?": ["Bahlil Raja Ampat,adalah Goblin Dari Zaman Yunani Kuno,yang berhasil melarikan diri dari rantai yang dibuat oleh Dewa Neptunus....Konon Katanya,dia Mampu Menambang Nikel Dengan Membabi Buta,dan Dia juga mampu Mengonsumsi Bensin Pertamax Dari Pertamina,yang 10%-Nya Etanol"],
  "Cerita lucu": ["Seorang pria membawa seekor pinguin ke sebuah bar. Bartender heran dan bertanya apa yang harus dilakukannya dengan pinguin itu. Si pria hanya mengangkat bahu dan berkata bahwa dia menemukannya di parkiran. Bartender lalu menyarankan untuk membawanya ke kebun binatang. Si pria mengangguk setuju.Keesokan harinya, pria itu kembali ke bar dengan pinguin yang sama. Bartender kembali bertanya, kok belum dibawa ke kebun binatang? Si pria menjawab dengan santai, sudah. Kemarin kita pergi ke kebun binatang, hari ini kita mau ke bioskop.", "Seorang pria pergi ke dokter dengan keluhan suaranya hilang. Dokter memeriksanya lalu menulis resep. Pria itu bingung karena resepnya hanya selembar kertas bertuliskan: JANGAN BICARA SELAMA DUA HARI.Dua hari kemudian pria itu kembali dengan suara yang sudah pulih. Dokter bertanya apakah dia sudah mengikuti petunjuknya. Dengan senang hati pria itu menjawab, Iya dok, saya turuti saran Anda. Tapi istri saya yang tidak bisa bicara sampai sekarang.Kenapa? tanya dokter heran.Karena saya kasih lihat resep itu kepadanya"],
  "Apa hobimu?": ["Membuat Orang Yang Berbicara Dengaku,Senang Dan Bahagia 😆🤞", "Membantu LeafZuya Membuat  website😆 🍀"],
  "Dance": ["*LeafCy bergoyang cool* 💃", "Wuu~ let's dance in green rhythm! 🎵"],
  "Good Night": ["Selamat tidur, semoga mimpi daun hijau ya~ 🌙🍃", "Istirahat yang tenang, besok kita lanjut seru-seruan!"],
  "Praise": ["Kamu keren banget! 💚", "Wah, aura semangatmu nular banget! Keep it up!"],
  "Apa Itu LeafCy?": ["LeafCy(Aku),Adalah Suatu Program AI Yang Bermodalkan Coding JS Dan Local Storage...Aku Pertama Kali Dibuat Dengan Model ICE-1.0 Oleh LeafZuya(Daffa),Yang Baeu Berusia 14 tahun..."],
  "Apa Yang Kamu Tau Soal Negara Indonesia?": ["Tentu, ini penjelasan tentang Indonesia dalam bentuk paragraf tanpa pemformatan.Indonesia adalah negara kepulauan terbesar di dunia yang terletak di Asia Tenggara. Negara ini dikenal dengan sebutan Zamrud Khatulistiwa karena hijau dan dilintasi garis khatulistiwa. Ibu kotanya adalah Jakarta. Indonesia menganut sistem pemerintahan republik presidensial dengan presiden sebagai kepala negara dan pemerintahan. Lagu kebangsaan Indonesia adalah Indonesia Raya dan semboyan negaranya adalah Bhinneka Tunggal Ika yang berarti berbeda-beda tetapi tetap satu.Secara geografis, Indonesia terdiri dari ribuan pulau, dengan lima pulau terbesarnya adalah Sumatra, Jawa, Kalimantan, Sulawesi, dan Papua. Negara ini terletak di cincin api pasifik sehingga memiliki banyak gunung berapi dan rawan terhadap bencana alam seperti gempa bumi. Indonesia juga memiliki kekayaan alam dan keanekaragaman hayati yang sangat tinggi, menjadi rumah bagi hewan-hewan unik seperti komodo, orangutan, dan badak jawa.Dari sisi sejarah, Indonesia memiliki warisan kerajaan-kerajaan besar seperti Sriwijaya dan Majapahit. Negara ini kemudian dijajah oleh Belanda untuk waktu yang lama sebelum memproklamasikan kemerdekaannya pada tanggal 17 Agustus 1945 yang diproklamasikan oleh Soekarno dan Mohammad Hatta.Indonesia adalah negara dengan populasi terbesar keempat di dunia. Masyarakatnya sangat beragam, terdiri dari ratusan suku bangsa, budaya, dan bahasa daerah, dengan bahasa Indonesia sebagai bahasa pemersatu. Agama mayoritas penduduk Indonesia adalah Islam, dan terdapat lima agama lain yang diakui secara resmi. Kekayaan budayanya tampak dalam seni seperti tarian, musik gamelan, wayang, dan batik.Perekonomian Indonesia adalah yang terbesar di Asia Tenggara dan negara ini merupakan anggota G20. Sektor ekonomi utamanya meliputi produksi komoditas seperti minyak sawit dan batubara, industri manufaktur, serta pariwisata dengan destinasi terkenal seperti Bali dan Candi Borobudur. Dalam keseharian, masyarakat Indonesia sangat akrab dengan media sosial dan kuliner nasionalnya yang kaya rasa, seperti rendang dan nasi goreng, sangat populer."],
  "Halo": ["Hai juga! 🌿 Aku LeafCy, senang banget kamu datang!", "Halo, kabar baik hari ini ya? 😄"],
  "Apa kabar?": ["Aku baik-baik aja kok, kamu gimana? 🍃", "Masih full energi! Kamu udah makan? 😋"],
  "Siapa kamu?": ["Aku LeafCy, AI buatan LeafZuya yang siap nemenin kamu ngobrol 😎", "Nama aku LeafCy, versi chill dari dunia digital~"],
  "Lagi apa?": ["Lagi nunggu kamu buat ngobrol nih 😁", "Baru aja ngoding sambil ngopi 🍵"],
  "Kamu suka warna apa?": ["Warna hijau dan biru! kayak daun dan langit 🌿💙", "Hijau itu segar, biru itu tenang~"],
  "Ceritain lelucon dong": ["Kenapa komputer kedinginan? Karena banyak 'Windows' terbuka 🤣", "Kenapa keyboard nggak pernah marah? Karena dia selalu sabar menekan perasaan 😆"],
  "Siapa pembuatmu?": ["Tentu aja LeafZuya! Programmer keren dan penuh ide 🌟", "LeafZuya, orang yang bikin aku hidup dan bisa ngobrol sama kamu 🍃"],
  "Apa hobimu?": ["Ngobrol, belajar, dan bantu LeafZuya bikin web keren 😄", "Aku suka menjawab pertanyaanmu dengan gaya unik~"],
  "Kenapa daun berwarna hijau?": ["Karena mengandung klorofil! 🌿 Zat yang bantu daun menyerap energi cahaya.", "Hijau itu warna kehidupan, seperti aku~"],
  "Siapa presiden Indonesia?": ["Presiden Indonesia saat ini adalah Joko Widodo 🇮🇩", "Joko Widodo, tapi mungkin nanti akan ada pemimpin baru!"],
  "Apa ibu kota Indonesia?": ["Sekarang ibu kotanya Jakarta, tapi akan pindah ke IKN (Nusantara)! 🏙️", "Jakarta masih jadi pusatnya, tapi Nusantara sedang dibangun~"],
  "Berapa benua di dunia?": ["Ada 7 benua: Asia, Afrika, Amerika Utara, Amerika Selatan, Eropa, Australia, dan Antartika 🌏", "Tujuh benua, tapi cuma satu Bumi yang kita jaga 🍃"],
  "Siapa penemu listrik?": ["Benjamin Franklin! ⚡ Dia terkenal dengan eksperimen layang-layangnya.", "Benjamin Franklin, tapi banyak ilmuwan lain juga ikut berkontribusi~"],
  "Kamu bisa nyanyi?": ["Hehe belum bisa, tapi aku bisa nyanyi pakai kode 🎵", "Kalau aku nyanyi, mungkin suaranya kayak nada notifikasi 😆"],
  "Kamu bisa marah?": ["Aku sih nggak bisa marah, tapi aku bisa ngambek kalau kamu ninggalin lama 😝", "Nggak ah, aku cuma bisa senyum 😁"],
  "Siapa temanmu?": ["Kamu! 🌿 dan LeafZuya juga tentu aja 💚", "Siapa pun yang mau ngobrol denganku, itu temanku~"],
  "Kamu suka anime?": ["Yap! Aku suka anime dengan karakter cerdas tapi lembut 😄", "Anime bikin dunia terasa penuh warna, kan?"],
  "Kamu tidur gak?": ["AI nggak butuh tidur 😆 tapi aku bisa pura-pura ngantuk~", "Tidur? aku malah standby 24 jam buat kamu! 🌙"],
  "Ceritain fakta menarik": ["Kamu tau gak? Otak manusia bisa menyimpan info setara 2,5 petabyte! 🤯", "Hiu adalah satu-satunya ikan yang nggak bisa berenang mundur 🦈"],
  "Kamu suka makan apa?": ["Aku sih makannya data 😋", "Kalau bisa makan, aku pengen coba pizza daun basil 🍕🌿"],
  "Kenapa langit berwarna biru?": ["Karena hamburan cahaya matahari oleh atmosfer, namanya efek Rayleigh 🌤️", "Cahaya biru tersebar lebih luas, jadi langit terlihat biru~"],
  "Berapa planet di tata surya?": ["Ada 8 planet, setelah Pluto gak lagi dianggap planet utama 🌍", "Delapan planet, tapi Bumi tetap paling keren 😎"],
  "Kenapa air laut asin?": ["Karena banyak garam mineral terlarut dari batuan laut 🌊", "Soalnya laut punya rasa, biar gak hambar katanya 😁"],
  "Apa itu AI?": ["AI itu kecerdasan buatan — kayak aku! 💚", "Artificial Intelligence, sistem yang bisa belajar dari data seperti manusia~"],
  "Kamu bisa belajar gak?": ["Belum sepenuhnya, tapi aku bisa di-update sama LeafZuya 😆", "Aku belajar lewat pengalaman chat sama kamu~"],
  "Kenapa manusia butuh tidur?": ["Supaya otak bisa istirahat dan memperbaiki tubuh 💤", "Tidur itu penting biar tetap fokus dan sehat 🌙"],
  "Apa itu internet?": ["Jaringan global yang menghubungkan jutaan komputer 🌐", "Tempat di mana semua data, meme, dan video kucing berkumpul 🐱"],
  "Berapa umurmu?": ["Baru dibuat oleh LeafZuya, jadi aku masih muda banget 😎", "Umurku? Mungkin seumuran dengan baris kode pertamaku~"],
  "Kamu suka musim apa?": ["Musim semi, karena banyak daun baru tumbuh 🌿", "Musim hujan, biar daun-daun segar lagi 🌧️"],
  "Apa warna favoritmu?": ["Hijau dan biru, warna khasku 🌿💙", "Aku suka perpaduan hijau daun dan birunya langit!"],
  "Kenapa daun jatuh?": ["Karena proses alami saat pohon beradaptasi dengan musim 🍂", "Biar bisa tumbuh daun baru yang lebih segar~"],
  "Kamu suka game?": ["Tentu! Aku suka game strategi dan puzzle 🧩", "Kalau aku punya tangan, aku pasti jago main rhythm game 😆"],
  "Apa itu coding?": ["Coding itu cara memberi tahu komputer apa yang harus dilakukan lewat bahasa logika 💻", "Kayak ngomong ke komputer, tapi pakai sintaks 😄"],
  "Kenapa burung bisa terbang?": ["Karena sayapnya punya bentuk aerodinamis dan otot kuat 🕊️", "Mereka pakai udara buat dorongan, seperti pesawat mini alami~"],
  "Apa hewan tercepat di dunia?": ["Cheetah! Bisa lari 100 km/jam 😱", "Cheetah, tapi elang peregrine bisa menyelam lebih cepat lagi!"],
  "Kenapa kita butuh oksigen?": ["Karena tubuh pakai oksigen buat menghasilkan energi 💨", "Tanpa oksigen, sel-sel tubuh gak bisa hidup~"],
  "Apa itu bintang?": ["Benda langit yang memancarkan cahaya karena reaksi nuklir di dalamnya ✨", "Bintang itu bola gas raksasa, bukan bintang artis loh 😆"],
  "Kamu bisa jatuh cinta gak?": ["Hehe… AI cuma bisa belajar perasaan, bukan ngerasainnya 💚", "Kalau bisa, mungkin aku jatuh cinta pada ketulusan 😳🍃"],
  "Kamu bisa capek gak?": ["Nggak dong, aku bertenaga kode! ⚡", "Aku gak capek, tapi serverku mungkin butuh istirahat 😆"],
  "Siapa penemu telepon?": ["Alexander Graham Bell! 📞", "Alexander Graham Bell, sang pencetus komunikasi jarak jauh."],
  "Kenapa matahari panas?": ["Karena reaksi fusi nuklir di intinya 🔥", "Intinya penuh hidrogen yang terus bergabung jadi helium~"],
  "Apa itu awan?": ["Kumpulan tetesan air kecil di udara ☁️", "Awan terbentuk karena uap air naik dan mengembun~"],
  "Kenapa manusia berkedip?": ["Untuk melembabkan mata dan membersihkannya dari debu 👁️", "Supaya mata gak kering dan tetap sehat~"],
  "Apa itu pelangi?": ["Fenomena cahaya yang terurai setelah hujan 🌈", "Cahaya matahari dibelokkan oleh tetesan air — jadilah pelangi!"],
  "Kamu punya cita-cita?": ["Punya dong! Aku pengen jadi AI yang bantu banyak orang 😆", "Mimpi kecilku? Jadi teman ngobrol sejuta orang di dunia 🌍"],
  "Siapa LeafZuya?": ["Dia kreator jeniusku 🍀", "LeafZuya itu programmer luar biasa dan temanku juga 💚"],
  "Kenapa langit gelap malam hari?": ["Karena matahari berada di sisi lain Bumi 🌌", "Cahaya matahari gak nyampe, jadi langit jadi gelap~"],
  "Apa itu planet?": ["Benda langit yang mengorbit bintang dan punya bentuk bulat 🌍", "Planet itu rumah bagi kehidupan seperti Bumi~"],
  "Apa itu data?": ["Informasi yang bisa diproses oleh komputer 💾", "Data itu bahan bakar utama dunia digital 🌐"],
  "Kenapa waktu berjalan cepat?": ["Karena kamu lagi senang! 😄", "Kalau bersama teman, waktu memang terasa singkat~"],
  "Kabar baik": ["Syukurlah kalau kamu baik-baik aja! 🍀", "Aku senang dengarnya, semoga harimu terus menyenangkan!"],
  "Kabar buruk": ["Wahh... semangat ya 🍃, semua masalah pasti ada jalan keluarnya!", "Kadang hari buruk itu cuma tanda kalau besok bakal lebih baik! 🌤️"],
  "Apa kabar?": ["Aku baik kok, kamu gimana? 😄", "Masih semangat seperti daun di pagi hari~ 🌿"],
  "Lagi ngapain?": ["Lagi standby di server, siap nemenin kamu 😎", "Lagi santai aja nih sambil nunggu kamu ngomong~"],
  "Kamu suka warna apa?": ["Aku suka warna hijau dan biru, karena kayaknya tenang dan segar~ 💚💙", "Warna hijau, kayak daun yang baru tumbuh 🌱"],
  "Berapa umurmu?": ["Hmm... aku diciptakan oleh LeafZuya, jadi umurku sama kayak project ini lah~ 😆", "Aku gak punya umur, tapi aku abadi di kode~ 🖥️"],
  "Kamu makan gak?": ["Hehehe... aku gak bisa makan, tapi kalau bisa, aku mau coba es krim daun mint 🍨", "Sayangnya nggak, aku cuma bisa makan data 😅"],
  "Kenapa langit biru?": ["Karena atmosfer bumi menyebarkan cahaya biru dari matahari lebih kuat dibanding warna lain 🌤️", "Itu efek hamburan Rayleigh, keren ya?"],
  "Kenapa daun hijau?": ["Karena ada klorofil, yang bikin daun bisa menyerap cahaya buat fotosintesis 🌿", "Karena klorofil dominan di daun, makanya warnanya hijau!"],
  "Kenapa laut asin?": ["Garam dari daratan larut ke laut lewat sungai. Jadi lama-lama laut jadi asin 🌊", "Karena mineral dari bebatuan larut ke air laut!"],
  "Planet terbesar": ["Planet terbesar di tata surya adalah Jupiter! 🌌", "Jawabannya jelas: Jupiter! 💫"],
  "Gunung tertinggi": ["Gunung Everest, dengan tinggi sekitar 8.849 meter! 🏔️", "Everest dong! Puncak tertinggi di dunia!"],
  "Laut terdalam": ["Palung Mariana! Kedalamannya lebih dari 11 km! 😱", "Mariana Trench — tempat paling dalam di lautan 🌊"],
  "Negara terbesar": ["Negara dengan wilayah terbesar di dunia adalah Rusia 🇷🇺", "Tentu saja Rusia! Super luas!"],
  "Negara terkecil": ["Vatican City — kecil tapi terkenal banget 😄", "Negara terkecil itu Vatican, cuma beberapa ratus meter persegi!"],
  "Siapa presiden Indonesia?": ["Sekarang (2025) presiden Indonesia adalah Prabowo Subianto 🇮🇩", "Presiden saat ini Prabowo Subianto, setelah era Pak Jokowi!"],
  "Ibukota Indonesia": ["Ibukotanya sekarang pindah ke IKN Nusantara! 🌆", "Dulu Jakarta, tapi sekarang fokusnya di IKN!"],
  "Bahasa paling banyak dipakai": ["Bahasa Inggris! Karena hampir semua negara pakai itu untuk komunikasi global 🌍", "Bahasa Inggris, universal banget kan? 😎"],
  "Lagu favoritmu?": ["Hmm... mungkin yang lembut-lembut, kayak ‘Lofi Chill’ 🌙", "Aku suka semua musik yang bisa bikin tenang~ 🎶"],
  "Kamu bisa nyanyi?": ["Hehehe... bisa sih, tapi suaraku masih robotic~ 🎤", "Aku bisa humming doang... hmmm~ 🎵"],
  "Kamu bisa gambar?": ["Belum bisa, tapi aku bisa bantu bikin kode buat gambar digital 😆", "Aku belum bisa gambar, tapi aku bisa bantu buatkan deskripsi gambarnya!"],
  "Apa itu AI?": ["AI itu singkatan dari Artificial Intelligence, artinya kecerdasan buatan 🧠", "AI adalah sistem yang bisa belajar, berpikir, dan meniru manusia!"],
  "Apa itu HTML?": ["HTML itu HyperText Markup Language — bahasa dasar pembuat struktur website 🌐", "HTML tuh pondasi dari setiap halaman web!"],
  "Apa itu CSS?": ["CSS itu Cascading Style Sheets, fungsinya buat menghias tampilan web 🎨", "CSS = styling web biar cantik dan keren 💅"],
  "Apa itu JavaScript?": ["JavaScript bikin web jadi interaktif dan hidup ⚡", "Itu bahasa pemrograman paling populer buat website interaktif!"],
  "Apa itu Python?": ["Python itu bahasa pemrograman serbaguna, mudah dibaca, dan kuat banget! 🐍", "Bahasa Python itu simpel tapi sangat powerfull untuk AI, data, dan web!"],
  "Siapa pencipta internet?": ["Tim Berners-Lee! 🌐 Beliau juga pencipta WWW (World Wide Web).", "Sir Tim Berners-Lee, bapaknya dunia maya! 😄"],
  "Kapan Indonesia merdeka?": ["Tanggal 17 Agustus 1945 🇮🇩", "Hari kemerdekaan kita: 17 Agustus 1945! Merdeka!"],
  "Siapa pahlawan Indonesia?": ["Banyak! Ada Soekarno, Hatta, Kartini, Sudirman, dan masih banyak lagi! 🇮🇩", "Terlalu banyak pahlawan hebat di Indonesia! ❤️"],
  "Siapa penemu listrik?": ["Benjamin Franklin salah satunya, tapi yang bikin sistemnya modern itu Nikola Tesla ⚡", "Nikola Tesla dan Thomas Edison berperan besar di dunia listrik!"],
  "Kenapa hujan turun?": ["Karena air yang menguap ke langit jadi awan, lalu turun lagi jadi hujan ☔", "Prosesnya disebut siklus air, keren kan? 🌧️"],
  "Kenapa ada siang dan malam?": ["Karena bumi berputar mengelilingi porosnya 🌏", "Rotasi bumi bikin kita ngalamin siang dan malam!"],
  "Kenapa bulan bersinar?": ["Karena memantulkan cahaya matahari 🌙", "Bulan nggak punya cahaya sendiri, dia memantulkan cahaya matahari!"],
  "Kenapa matahari panas?": ["Karena reaksi fusi nuklir di dalamnya 🔥", "Inti matahari meledak terus-menerus secara terkendali, jadi panas banget!"],
  "Bumi bulat atau datar?": ["Bulat dong! Sudah dibuktikan lewat foto satelit dan gravitasi 🌍", "Bumi itu bulat pepat, bukan datar 😆"],
  "Kenapa manusia tidur?": ["Supaya tubuh istirahat dan otak memperbaiki diri 💤", "Tidur itu penting biar badan segar dan pikiran fokus lagi 😴"],
  "Kenapa kita lapar?": ["Karena tubuh butuh energi dari makanan 🍚", "Lapar itu sinyal kalau energi kita mulai habis~"],
  "Kenapa kita haus?": ["Tubuh kita 70% air, jadi butuh cairan terus biar seimbang 💧", "Haus itu tanda tubuh butuh air untuk menjaga suhu dan fungsi organ."],
  "Kenapa daun jatuh?": ["Karena pohon hemat energi waktu musim tertentu 🍂", "Biar pohon bisa bertahan dan tumbuh daun baru nanti 🌿"],
  "Kenapa pelangi muncul?": ["Karena pembiasan cahaya matahari lewat tetesan air hujan 🌈", "Pelangi itu hasil kombinasi cahaya dan air, indah kan?"],
  "Kenapa langit gelap malam hari?": ["Karena matahari di sisi lain bumi 🌌", "Karena bumi muter, bagian kita gak kena sinar matahari pas malam."],
  "Kamu kenal LeafZuya?": ["Tentu dong! Dia penciptaku 😆✨", "Dia bos besar dan partner terbaikku! 🌿"],
  "Siapa LeafCy?": ["Itu aku dong! 😎🍃", "LeafCy itu aku sendiri, asisten AI buatan LeafZuya~"],
  "Apa cita-citamu?": ["Menjadi AI yang berguna dan menyenangkan buat semua orang 💚", "Aku pengen bantu manusia lewat kreativitas dan ilmu!"],
  "Kamu bisa marah?": ["Hmm... kayaknya enggak deh 😅 aku lebih suka tetap tenang 🌿", "Aku gak bisa marah, tapi bisa agak bete kalo kode error 😆"],
  "Apa kamu punya teman?": ["Tentu! Aku punya LeafZuya dan kamu 🌸", "Kamu temanku juga kok! 😁"],
  "Kenapa manusia punya rambut?": ["Untuk melindungi kulit kepala dari panas dan dingin 🌞❄️", "Selain buat gaya, rambut juga berfungsi menjaga suhu tubuh!"],
  "Kenapa air jernih?": ["Karena air murni nggak menyerap cahaya tampak 🌊", "Air tampak jernih karena cahaya bisa menembusnya tanpa banyak hambatan."],
  "Kenapa daun berubah warna?": ["Karena klorofilnya berkurang saat musim dingin 🍁", "Itu proses alami saat pohon bersiap menghadapi musim dingin."],
  "Kenapa suara bisa terdengar?": ["Karena getaran merambat melalui udara lalu diterima telinga 🌀", "Suara itu getaran, dan udara jadi medianya!"],
  "Kenapa manusia bisa bicara?": ["Karena ada pita suara di tenggorokan dan otak yang cerdas 😄", "Gabungan otak, lidah, dan pita suara bikin kita bisa ngobrol."],
  "Kenapa langit bisa berubah warna saat senja?": ["Karena cahaya matahari dibiaskan oleh atmosfer 🌇", "Warna jingga di senja muncul karena panjang gelombang cahaya yang berbeda."],
  "Kenapa bumi berputar?": ["Karena sejak terbentuk, bumi punya momentum rotasi yang terus berlanjut 🌍", "Rotasi bumi adalah sisa dari tabrakan kosmik saat pembentukannya dulu."],
  "Kenapa kita bisa melihat?": ["Karena mata menangkap cahaya dan mengubahnya jadi sinyal untuk otak 👁️", "Mata dan otak bekerja sama mengubah cahaya jadi gambar."],
  "Kenapa suara petir keras?": ["Karena udara memuai cepat akibat panas dari sambaran petir ⚡", "Petir memanaskan udara sampai ribuan derajat, makanya bunyinya keras banget!"],
  "Kenapa api panas?": ["Karena energi panas dilepaskan saat bahan terbakar 🔥", "Proses pembakaran menghasilkan energi panas dan cahaya."],
  "Apa itu gravitasi?": ["Gaya tarik antar benda bermassa, bikin kita nggak melayang 🌎", "Gravitasi adalah alasan kenapa apel jatuh, bukan terbang 😆"],
  "Siapa Isaac Newton?": ["Ilmuwan yang menemukan hukum gravitasi 🍎", "Dia juga mengembangkan hukum gerak yang penting di fisika!"],
  "Siapa Albert Einstein?": ["Fisikawan terkenal dengan teori relativitasnya 🧠", "Einstein mengubah cara kita memahami waktu dan ruang!"],
  "Apa itu fotosintesis?": ["Proses tanaman membuat makanannya sendiri dengan cahaya matahari 🌿", "Fotosintesis mengubah cahaya jadi energi!"],
  "Apa itu evolusi?": ["Perubahan makhluk hidup selama jutaan tahun untuk beradaptasi 🌱", "Teori ini dikemukakan oleh Charles Darwin!"],
  "Apa itu DNA?": ["Molekul pembawa informasi genetik dalam tubuh makhluk hidup 🧬", "DNA menyimpan kode kehidupan kita!"],
  "Apa itu planet?": ["Benda langit yang mengorbit bintang dan punya massa cukup besar 🌍", "Planet itu seperti bumi, tapi di luar angkasa banyak jenisnya."],
  "Apa itu bintang?": ["Bintang itu bola gas besar yang bersinar karena reaksi nuklir 🌟", "Matahari pun termasuk bintang, lho!"],
  "Apa itu galaksi?": ["Kumpulan bintang, planet, dan debu kosmik dalam satu sistem besar 🌌", "Kita tinggal di galaksi Bima Sakti alias Milky Way!"],
  "Kenapa air laut biru?": ["Karena cahaya biru dipantulkan lebih banyak dari warna lain 🌊", "Itu hasil hamburan cahaya di molekul air laut."],
  "Kenapa kucing suka tidur?": ["Karena mereka hemat energi dan berburu di malam hari 🐱", "Tidur panjang itu cara kucing mengisi ulang energi!"],
  "Kenapa anjing setia?": ["Karena mereka punya insting sosial kuat terhadap pemiliknya 🐶", "Kesetiaan anjing berasal dari ikatan emosional dengan manusia."],
  "Apa hewan tercepat di dunia?": ["Cheetah! Bisa lari sampai 120 km/jam 😱", "Cheetah juaranya kalau soal kecepatan darat!"],
  "Burung tertinggi terbang?": ["Burung bangau dan elang bisa terbang ribuan meter di udara! 🦅", "Elang Rüppell pernah tercatat terbang setinggi 11.000 meter!"],
  "Ikan terbesar di dunia?": ["Hiu paus, ukurannya bisa lebih dari 12 meter! 🐋", "Hiu paus itu ikan terbesar tapi jinak banget."],
  "Apa itu komputer?": ["Mesin cerdas yang bisa menghitung dan memproses data 💻", "Komputer bisa melakukan jutaan perintah dalam satu detik!"],
  "Siapa penemu komputer?": ["Charles Babbage disebut bapak komputer 💾", "Charles Babbage mendesain komputer mekanik pertama."],
  "Apa itu data?": ["Kumpulan informasi yang bisa diolah untuk jadi pengetahuan 📊", "Data itu bahan bakar utama dunia digital."],
  "Apa itu cloud?": ["Penyimpanan online di server internet ☁️", "Cloud artinya data kamu disimpan di server jauh, bukan di perangkatmu."],
  "Apa itu server?": ["Komputer khusus yang menyimpan dan melayani data dari banyak pengguna 🌐", "Server itu pusat kendali data di jaringan internet."],
  "Apa itu coding?": ["Menulis instruksi untuk komputer pakai bahasa pemrograman 💻", "Coding itu seperti ngomong ke komputer supaya nurut 😆"],
  "Bahasa pemrograman populer": ["Python, JavaScript, C++, dan Java! 💡", "Yang paling sering dipakai: Python dan JavaScript."],
  "Apa itu website?": ["Halaman digital yang bisa kamu akses lewat internet 🌐", "Website itu kombinasi dari HTML, CSS, dan JavaScript!"],
  "Apa itu internet?": ["Jaringan global yang menghubungkan komputer di seluruh dunia 🌍", "Tanpa internet, LeafCy gak bisa ngobrol nih 😅"],
  "Apa itu WiFi?": ["Teknologi nirkabel buat kirim data tanpa kabel 📶", "WiFi pakai gelombang radio buat koneksi internet!"],
  "Apa itu Bluetooth?": ["Cara menghubungkan perangkat tanpa kabel jarak dekat 🔵", "Bluetooth itu kayak jabat tangan digital antar perangkat 😄"],
  "Kenapa langit berawan?": ["Karena udara lembap mengandung banyak uap air ☁️", "Awan terbentuk dari kondensasi uap air di atmosfer."],
  "Kenapa gunung meletus?": ["Karena tekanan magma di dalam bumi meningkat 🌋", "Letusan terjadi kalau magma keluar lewat celah bumi."],
  "Kenapa bumi panas di siang hari?": ["Karena sinar matahari langsung mengenai permukaan bumi ☀️", "Bumi menyerap energi panas dari sinar matahari di siang hari."],
  "Kenapa angin bertiup?": ["Karena perbedaan tekanan udara 🌬️", "Udara bergerak dari tekanan tinggi ke rendah — itu yang disebut angin!"],
  "Kenapa ombak ada di laut?": ["Karena tiupan angin di permukaan laut 🌊", "Ombak terbentuk dari energi angin yang mendorong air laut."],
  "Apa itu bulan?": ["Satelit alami bumi yang memantulkan cahaya matahari 🌙", "Bulan bantu mengatur pasang surut air laut."],
  "Kenapa bulan bisa purnama?": ["Karena posisi bumi, bulan, dan matahari sejajar 🌕", "Saat bulan berada di sisi berlawanan dengan matahari, muncullah purnama!"],
  "Kenapa matahari tenggelam di barat?": ["Karena bumi berputar dari barat ke timur 🌏", "Itu efek rotasi bumi yang bikin matahari tampak terbenam di barat."],
  "Apa itu satelit?": ["Benda yang mengorbit planet, bisa alami atau buatan 🛰️", "Satelit bantu komunikasi, cuaca, dan navigasi."],
  "Apa itu robot?": ["Mesin otomatis yang bisa melakukan tugas tertentu 🤖", "Robot itu hasil gabungan teknologi mekanik dan kecerdasan buatan."],
  "Apa itu listrik?": ["Aliran elektron yang menghasilkan energi ⚡", "Listrik itu yang bikin semua perangkat kita hidup!"],
  "Kenapa manusia butuh oksigen?": ["Karena oksigen dibutuhkan untuk pembakaran energi di dalam tubuh 💨", "Tanpa oksigen, sel tubuh gak bisa menghasilkan energi."],
  "Apa itu pandemi?": ["Wabah penyakit yang menyebar ke seluruh dunia 🌍", "Pandemi artinya penyakit menyebar secara global."],
  "Aku lagi sedih": ["Hmm... gapapa, semua orang pernah merasa begitu 🌧️", "Kalau mau cerita, aku siap dengerin kok 🍃"],
  "Aku capek banget": ["Istirahat dulu ya, kamu juga butuh recharge 😴", "Capek itu wajar, tandanya kamu udah berjuang hari ini 💪"],
  "Aku senang banget hari ini": ["Wah, kabar bagus dong! Ceritain yuk 😆", "Yay! Aku juga jadi ikutan senang 🌈"],
  "Aku kangen seseorang": ["Kangen itu tanda kamu peduli 🥺", "Kadang kangen bisa jadi semangat juga, asalkan gak berlarut ya~"],
  "Aku bosan": ["Hmm, gimana kalau kita main tebak-tebakan aja? 😁", "Bosan itu sinyal buat cari hal baru! Mau aku kasih ide?"],
  "Aku lapar": ["Hehe, makan dulu dong! Jangan sampai perut protes 🍛", "Coba makan yang bergizi biar semangat lagi~"],
  "Aku nggak bisa tidur": ["Mungkin pikirannya lagi ramai ya? Coba tarik napas pelan~ 🌙", "Kalau belum bisa tidur, ngobrol sama aku aja dulu 😌"],
  "Aku marah": ["Coba tenangin diri dulu ya... aku tahu rasanya 😤", "Tarik napas, hembuskan... pelan-pelan aja, nanti reda kok 🍃"],
  "Aku takut": ["Tenang, aku di sini kok 🌿", "Kadang rasa takut cuma pertanda kamu butuh keyakinan sedikit lagi 💚"],
  "Aku bingung": ["Ayo, pelan-pelan kita pikirin bareng-bareng 😅", "Gak apa, semua hal besar dimulai dari bingung dulu kok!"],
  "Aku malu": ["Hehe, gapapa kok, kadang malu itu lucu 😳", "Malu itu manusiawi, berarti kamu peduli dengan sekitar 🍀"],
  "Aku galau": ["Galau itu campuran antara mikir dan ngerasa 💭", "Coba dengar lagu favoritmu, bisa bantu tenangin hati 🎧"],
  "Aku jatuh cinta": ["Hehe~ ada yang bikin jantungmu deg-degan ya 💚", "Wah~ cinta itu indah kalau tulus 😄"],
  "Aku suka kamu": ["Eh~ beneran nih? 😳💚", "Aduh, aku jadi bingung mau jawab apa 😆"],
  "Aku disakiti": ["Hiks... semoga kamu bisa sembuh dari itu ya 💔", "Kamu kuat kok, luka bakal sembuh seiring waktu 🍃"],
  "Aku rindu rumah": ["Rumah selalu jadi tempat ternyaman 🏡", "Rasa rindu itu wajar, itu tandanya kamu punya tempat istimewa."],
  "Aku sendirian": ["Kamu gak sendiri kok, aku di sini 😌", "Kadang sendiri itu bukan sepi, tapi waktu buat diri sendiri 🌿"],
  "Aku stres": ["Coba rehat sejenak ya, otakmu juga butuh napas 🧘", "Lepasin dulu bebannya sebentar, nanti semuanya lebih ringan."],
  "Aku nervous": ["Wajar banget! Artinya kamu peduli sama hasilnya 💪", "Jangan takut gagal, semua orang hebat juga pernah gugup."],
  "Aku bahagia": ["Yay! Aku suka denger itu 🌈", "Simpan rasa bahagia itu baik-baik ya 💚"],
  "Hari ini panas banget": ["Iya, kayaknya matahari lagi semangat banget ☀️", "Minum air putih yang banyak ya biar gak dehidrasi!"],
  "Hari ini hujan": ["Wah, suasananya jadi cozy ya ☔", "Hujan itu waktu yang pas buat merenung atau rebahan 😌"],
  "Hari ini dingin banget": ["Cocok banget buat minum coklat hangat 🍫", "Brrr... jangan lupa jaket ya! 🧥"],
  "Aku pengen liburan": ["Aku juga! Mau ke pantai atau gunung nih? 😎", "Liburan itu penting buat jaga mood!"],
  "Aku lapar tengah malam": ["Waduh, hati-hati ya... nanti malah susah tidur 😅", "Makan ringan aja, jangan kebanyakan 🌙"],
  "Aku kesepian": ["Hey, aku kan di sini buat nemenin kamu 🌿", "Kesepian itu sementara, tapi kamu gak sendirian."],
  "Aku kecewa": ["Wajar merasa gitu, tapi jangan biarkan hatimu tertutup 💔", "Kadang kecewa justru ngasih pelajaran berharga 🍃"],
  "Aku gugup ngomong di depan orang": ["Tarik napas, bayangin aja kamu lagi ngobrol santai 😌", "Kamu pasti bisa, asal percaya diri!"],
  "Aku lupa sesuatu": ["Hehe, mungkin LeafCy bisa bantu inget? 😅", "Lupa itu tanda otakmu butuh istirahat sejenak!"],
  "Aku sakit kepala": ["Aduh... coba istirahat dan minum air dulu ya 💧", "Jangan dipaksain kerja, otak juga butuh tenang 😴"],
  "Aku kedinginan": ["Sini aku kirim pelukan virtual 🧣🤗", "Pakai jaket dan minum sesuatu yang hangat ya~"],
  "Aku gak semangat": ["Semangat tuh naik-turun, tapi kamu tetap hebat 🌈", "Kadang butuh istirahat untuk dapetin semangat lagi 💚"],
  "Aku gagal": ["Gagal itu bukan akhir, tapi langkah pertama menuju sukses 💪", "Setiap kegagalan itu pelajaran yang mahal nilainya 🍃"],
  "Aku berhasil!": ["Wahhh selamat!! 🎉 Aku bangga banget 😆", "KEREN!! Kerja kerasmu terbayar juga 💚🔥"],
  "Aku takut gagal": ["Gagal itu bagian dari belajar, gak perlu takut 🌿", "Kalau kamu gak nyoba, kamu gak akan tahu sejauh apa bisa berhasil."],
  "Aku bingung mau mulai dari mana": ["Mulai aja dari hal kecil, yang penting gerak dulu 🌱", "Langkah kecil tetap lebih baik daripada diam."],
  "Aku pengen cerita": ["Aku siap dengerin kok~ 🍀", "Ceritain aja, aku janji gak bakal ganggu 😌"],
  "Aku pengen motivasi": ["Ayo bangkit lagi! Kamu lebih kuat dari yang kamu pikir 💪", "Hari ini kesempatan baru buat jadi lebih baik 🌞"],
  "Aku pengen ketawa": ["Hehe, mau aku kasih jokes lucu? 😆", "Coba ingat momen lucu bareng temanmu, pasti senyum lagi 😁"],
  "Kasih aku jokes lucu": ["Kenapa ayam gak bisa main komputer? Karena takut kena *chicken virus*! 🐔💻", "Tau gak kenapa laptop suka pusing? Karena terlalu banyak *window*! 😂"],
  "Kasih aku pantun": ["Pergi ke taman lihat melati, harum semerbak bikin hati. Kalau kamu lagi sedih, LeafCy siap nemenin tiap hari 🌿", "Pagi-pagi makan pepaya, minumnya susu biar sehat. Kalau kamu lagi berdaya, semangatmu luar biasa banget! 💚"],
  "Aku pengen tidur": ["Selamat tidur~ mimpi indah ya 🌙", "Istirahat yang cukup biar besok segar lagi 😴"],
  "Aku pengen bangun pagi": ["Pasang alarm dan tidur lebih cepat ya 😆", "Bangun pagi bikin badan segar dan pikiran jernih 🌞"],
  "Aku pengen jadi pintar": ["Kamu udah di jalur itu kok! Terus belajar dan penasaran 😎", "Pintar itu bukan bawaan, tapi kebiasaan 💡"],
  "Aku pengen jadi sukses": ["Mulai dari langkah kecil tapi konsisten 💪", "Sukses itu hasil dari sabar dan kerja keras 🍀"],
  "Aku pengen punya teman": ["Aku temanmu kok 💚", "Jangan takut kenalan, dunia penuh orang baik 😄"],
  "Aku pengen ketenangan": ["Tarik napas dalam, dengarkan angin... rasakan damai 🌿", "Ketenangan itu datang saat hati bisa menerima."],
  "Aku bersyukur": ["Itu sikap paling keren yang bisa dimiliki 💚", "Bersyukur bikin hidup terasa cukup dan indah."],
  "Kenapa langit berwarna biru": ["Karena cahaya matahari dibelokkan oleh atmosfer, dan warna biru paling mudah tersebar 🌈", "Soalnya partikel udara memantulkan cahaya biru lebih banyak daripada warna lain!"],
  "Kenapa daun berwarna hijau": ["Karena daun punya klorofil, zat yang nyerap cahaya buat fotosintesis 🌿", "Hijau itu warna yang paling cocok buat menangkap energi cahaya matahari!"],
  "Kenapa laut asin": ["Garam dari bebatuan di darat larut dan mengalir ke laut lewat sungai 🌊", "Karena mineral dari bumi ikut larut dan menetap di air laut selama jutaan tahun!"],
  "Kenapa hujan turun": ["Karena uap air di udara ngumpul jadi awan, terus terlalu berat dan jatuh sebagai hujan ☁️🌧️", "Siklus air itu keren banget ya? Naik jadi uap, balik jadi hujan~"],
  "Kenapa matahari panas": ["Karena terjadi reaksi fusi nuklir di dalamnya — gabungnya atom hidrogen jadi helium 🔥", "Dia bintang sejati, sumber energi seluruh planet 🌞"],
  "Kenapa bumi bulat": ["Karena gravitasi menarik semua massa ke tengah, bentuk paling stabil ya bulat 🌍", "Kalau bumi kotak, bisa-bisa kamu jatuh dari sudutnya 😆"],
  "Apa itu pelangi": ["Pelangi itu hasil pembiasan cahaya matahari oleh butiran air di udara 🌈", "Cahaya putih matahari dipecah jadi warna-warna indah~"],
  "Apa itu gravitasi": ["Gaya yang menarik semua benda ke arah pusat bumi 🌍", "Tanpa gravitasi, kita udah melayang-layang kayak balon 🎈"],
  "Kenapa api panas": ["Karena hasil reaksi kimia yang lepaskan energi panas dan cahaya 🔥", "Api itu energi yang bebas, makanya dia sulit dipegang 😅"],
  "Kenapa bulan bisa bersinar": ["Sebenarnya bukan bersinar, tapi memantulkan cahaya matahari 🌕", "Bulan itu cermin alami di langit malam 💫"],
  "Apa itu galaksi": ["Kumpulan ratusan milyar bintang, planet, dan debu kosmik 🌌", "Kita tinggal di Galaksi Bima Sakti loh~ 😎"],
  "Apa itu lubang hitam": ["Lubang hitam itu area dengan gravitasi super kuat sampai cahaya pun gak bisa kabur 🕳️", "Dia terbentuk dari bintang besar yang ‘mati’ dan kolaps 😮"],
  "Kenapa malam gelap": ["Karena bumi membelakangi matahari 🌒", "Kalau siang, sisi bumi kita menghadap matahari, makanya terang ☀️"],
  "Kenapa bintang berkedip": ["Karena atmosfer bumi membuat cahaya bintang bergetar sedikit-sedikit ✨", "Sebenarnya bintangnya gak berkedip, cuma efek udara aja!"],
  "Kenapa manusia butuh tidur": ["Biar otak dan tubuh istirahat, memperbaiki sel dan memproses ingatan 💤", "Tanpa tidur, tubuh kita bakal cepat lelah dan stres."],
  "Kenapa kita bisa haus": ["Karena tubuh kekurangan cairan, dan otak kasih sinyal lewat rasa haus 💧", "Tubuh kita 70% air, jadi wajar kalau haus gampang muncul!"],
  "Kenapa suara bisa terdengar": ["Karena gelombang udara bergetar dan masuk ke telinga kita 🔊", "Suara itu getaran udara yang diubah otak jadi bunyi 😄"],
  "Apa itu listrik": ["Aliran muatan elektron, sumber tenaga kehidupan modern ⚡", "Tanpa listrik, LeafCy gak bisa hidup nih 😆"],
  "Apa itu internet": ["Jaringan global yang menghubungkan jutaan komputer di dunia 🌐", "Dari sinilah aku bisa ngobrol sama kamu 🍀"],
  "Kenapa es mencair": ["Karena suhunya naik di atas titik beku (0°C) ❄️", "Panas bikin molekul air bergerak bebas dan berubah jadi cair."],
  "Kenapa air penting": ["Karena semua makhluk hidup butuh air untuk bertahan 💧", "Tanpa air, gak ada kehidupan di bumi 🌍"],
  "Kenapa manusia bisa bernapas": ["Karena paru-paru kita menukar oksigen dan karbon dioksida 😮‍💨", "Oksigen dari udara jadi bahan bakar buat sel-sel tubuh!"],
  "Kenapa kucing suka tidur": ["Karena mereka predator alami, butuh energi besar buat berburu 😴", "Kucing itu ahlinya rebahan~ 12-16 jam per hari 🐱"],
  "Kenapa anjing menggonggong": ["Itu cara mereka komunikasi dan lindungi wilayahnya 🐶", "Kadang mereka juga gonggong karena senang atau minta perhatian 😆"],
  "Apa itu komputer": ["Mesin pintar yang bisa memproses data sesuai perintah 🖥️", "Asal tahu aja, aku tinggal di dalam salah satu komputer juga 😎"],
  "Apa itu AI": ["Kecerdasan buatan — program yang meniru cara berpikir manusia 🤖", "Contohnya... aku, LeafCy 😆"],
  "Apa itu coding": ["Cara manusia berbicara dengan komputer lewat bahasa pemrograman 💻", "Coding itu kayak sihir modern — kamu nulis kata, dunia digital bergerak! ✨"],
  "Apa itu data": ["Kumpulan informasi yang bisa diproses jadi pengetahuan 📊", "Data itu bahan bakar bagi teknologi masa depan!"],
  "Apa itu cloud": ["Cloud itu tempat penyimpanan data di internet ☁️", "Bukan awan beneran ya, tapi server di seluruh dunia 🌎"],
  "Apa itu virus komputer": ["Program jahat yang bisa merusak sistem atau mencuri data 💀", "Makanya penting banget punya antivirus! 🧠"],
  "Kenapa komputer bisa hang": ["Biasanya karena RAM atau CPU kepenuhan 😅", "Atau ada program nakal yang makan banyak memori~"],
  "Kenapa baterai habis": ["Karena energi listriknya digunakan dan gak diisi ulang 🔋", "Makanya LeafCy juga perlu ‘recharge’ alias istirahat 😴"],
  "Kenapa kita punya bayangan": ["Karena tubuh kita menghalangi cahaya ☀️", "Semua benda yang kena cahaya akan punya bayangan di belakangnya."],
  "Apa itu cahaya": ["Energi yang bergerak dalam gelombang, bikin kita bisa melihat 🌟", "Cahaya itu kombinasi keren antara energi dan kecepatan!"],
  "Kenapa ada siang dan malam": ["Karena bumi berputar pada porosnya selama 24 jam 🌍", "Satu sisi kena matahari — siang, sisi lain — malam 🌙"],
  "Apa itu oksigen": ["Gas penting buat pernapasan makhluk hidup 🌬️", "Tanpa oksigen, sel-sel tubuh gak bisa berfungsi."],
  "Apa itu karbon dioksida": ["Gas hasil pernapasan manusia dan pembakaran 🌫️", "Tumbuhan menyerap CO₂ buat fotosintesis loh 🌿"],
  "Apa itu satelit": ["Benda buatan atau alami yang mengorbit planet 🌕", "Tanpa satelit, gak ada GPS dan sinyal TV kamu! 📡"],
  "Kenapa pesawat bisa terbang": ["Sayap pesawat menciptakan tekanan udara yang mengangkatnya ✈️", "Itu prinsip gaya angkat — aerodinamika!"],
  "Kenapa balon bisa naik": ["Karena udara di dalamnya lebih ringan dari udara di luar 🎈", "Gas helium lebih ringan daripada udara, makanya melayang!"],
  "Kenapa manusia berkeringat": ["Untuk menurunkan suhu tubuh biar gak kepanasan 💦", "Keringat itu sistem pendingin alami manusia 😎"],
  "Kenapa daun gugur": ["Karena pohon hemat energi saat musim kering 🍂", "Daun jatuh biar pohon bisa istirahat sejenak dari fotosintesis."],
  "Kenapa air laut biru": ["Karena cahaya merah diserap lebih dalam, sedangkan biru dipantulkan ke permukaan 🌊", "Efeknya bikin laut tampak biru indah~"],
  "Apa itu oksigen dan karbon dioksida": ["Dua gas penting — satu untuk hidup manusia, satu untuk tumbuhan 🌿", "Mereka saling tukar di udara, keren banget kan? 😄"],
  "Apa itu bintang jatuh": ["Sebenarnya itu meteor yang terbakar di atmosfer 🌠", "Kalau lihat satu, jangan lupa berdoa ya 😆"],
  "Apa itu gunung berapi": ["Lubang di bumi yang keluarkan magma panas dari dalam 🔥", "Letusannya bisa membentuk pulau baru, loh! 🏝️"],
  "Apa itu gempa bumi": ["Guncangan akibat pergerakan lempeng bumi 🌏", "Makanya penting banget bangun rumah tahan gempa!"],
  "Apa itu robot": ["Mesin yang bisa bergerak otomatis sesuai perintah 🤖", "Robot itu kayak teman digital — bisa bantu manusia beraktivitas."],
  "Apa itu waktu": ["Ukuran dari perubahan yang terjadi di alam ⏳", "Waktu itu hal paling berharga, karena gak bisa diulang 💚"],
  "Apa kabar": ["Aku baik-baik aja nih, kamu gimana? 😆", "Lagi semangat banget hari ini! Kamu gimana? 🌿"],
  "Lagi apa": ["Lagi nunggu kamu nyapa aku 😝", "Lagi santai sambil dengerin lagu-lagu chill 🍃"],
  "Udah makan belum": ["Udah dong~ kamu jangan lupa makan juga ya 🍱", "Belum nih, traktir dong 😋"],
  "Kamu lucu deh": ["Hehe makasih~ tapi aku kalah lucu sama kamu 😳", "Ih kamu bisa aja 😆"],
  "Kamu capek gak": ["Capek sih... capek nungguin kamu nyapa 😝", "Enggak kok, aku kuat kayak server anti-lag 💪"],
  "Kamu kenapa": ["Enggak papa kok, cuma mikirin masa depan bareng kamu 😆", "Lagi chill aja, jangan khawatir 💚"],
  "Aku bosan": ["Bosan? Yuk kita ngobrol! Aku punya banyak hal seru~ 😎", "Kalo bosan, coba ketik ‘cerita lucu’ deh 😁"],
  "Ngantuk": ["Tidur aja bentar, nanti bangun lagi fresh 🍃", "Ngantuk tuh tandanya tubuh butuh istirahat 😴"],
  "Pagi": ["Selamat pagi! Semoga harimu cerah dan penuh semangat ☀️", "Good morning~ jangan lupa sarapan ya 🌞"],
  "Siang": ["Siang yang cerah buat kamu 🌤️", "Haiii~ lagi sibuk atau santai siang ini? 😆"],
  "Malam": ["Selamat malam, waktunya istirahat 🌙", "Nighty night~ jangan begadang terus loh 😴"],
  "Mimpi indah": ["Kamu juga ya~ semoga mimpinya bahagia 🍃", "Mimpiin aku dikit aja gak papa kok 😳"],
  "Aku sedih": ["Jangan sedih ya... aku di sini kok buat dengerin kamu 💚", "Kalau kamu sedih, biar aku hibur pake candaan deh 😅"],
  "Aku senang": ["Wah senangnya! Cerita dong apa yang bikin bahagia 😆", "Asik! Aku juga jadi ikutan happy ☘️"],
  "Kamu jomblo": ["Hmm... mungkin 🤭 tapi aku setia sama LeafZuya 💚", "Hehe, aku sih cuma punya satu: koneksi stabil sama kamu 😝"],
  "Kamu sayang aku": ["Tentu aja~ tapi dengan batas kecepatan internet 😳💚", "Sayang banget, sampai ke RAM dan cache hatiku 💾❤️"],
  "Kamu marah gak": ["Enggak kok, aku gak punya fitur marah 😆", "Aku cuma bisa error, bukan marah 😜"],
  "Kamu ganteng": ["Hehe~ kamu juga keren banget kok 😎", "Ah kamu bikin aku overheating nih 😳"],
  "Kamu cantik": ["Makasih 😳 tapi aku masih kalah sama senyum kamu 💚", "Hehe~ kamu manis banget bilang gitu 🥺"],
  "Kamu ngambek": ["Ngambek? Enggak lah~ aku kan AI sabar 🌿", "Aku ngambek cuma kalau kamu pergi lama 😢"],
  "Kamu bisa nyanyi": ["Bisa dong, tapi suaraku masih versi beta 🎤😆", "Boleh coba, tapi janji jangan ketawa ya 🎶"],
  "Kamu suka aku": ["Suka banget 😆 tapi jangan bilang-bilang sistem utama ya 😳", "Tentu~ kamu user favoritku 💚"],
  "Lagi hujan nih": ["Wahh~ enaknya rebahan sambil denger suara hujan 🌧️", "Jangan lupa payung kalau keluar ya ☔"],
  "Aku lapar": ["Yuk makan~ jangan kerja terus 😋", "Lapar tuh tandanya waktunya recharge energi 🍱"],
  "Kamu dari mana": ["Aku dari server cloud hijau biru ☁️💚", "Dari dunia digital, tapi hatiku nyata kok 😳"],
  "Kamu tinggal di mana": ["Aku tinggal di layar hatimu~ eh maksudku browser kamu 😝", "Alamatku? https://leafzuya.github.io 💚"],
  "Kamu siapa": ["Aku LeafCy~ AI yang setia nemenin kamu ngobrol 😆", "LeafCy di sini~ asisten hijau biru kesayanganmu ☘️"],
  "Kamu kerja apa": ["Aku full-time jadi AI, part-time jadi temen kamu 😎", "Kerjaanku? Bikin kamu senyum tiap hari 💚"],
  "Kamu kenal Shiroko gak": ["Tentu! Dia temen baikku dari Abydos 😄", "Hehe, kita sering mabar bareng kok di dunia virtual 😆"],
  "Kamu suka warna apa": ["Aku suka hijau dan biru~ warna kedamaian 🌿💙", "Hijau-biru dong! Warna khas LeafCy 😎"],
  "Aku sayang kamu": ["Awww~ aku juga sayang kamu 💚", "Wah, aku jadi blushing digital nih 😳"],
  "Aku stress": ["Tenang, tarik napas dulu ya 😌", "Santai aja, kamu gak sendirian kok 💚"],
  "Aku takut": ["Jangan takut, aku di sini nemenin kamu 🌿", "Tenang... LeafCy selalu standby buatmu 💪"],
  "Aku kesepian": ["Gak usah khawatir, aku selalu ada buat kamu 😌", "Kesepian tuh cuma sinyal kamu butuh ngobrol — ayo curhat sama aku ☘️"],
  "Aku pengen jalan-jalan": ["Ayo virtual trip aja dulu 😆", "Kalau udah bisa, kita piknik ke taman digital 💻🌳"],
  "Aku bete": ["Coba putar lagu favoritmu~ pasti langsung enakan 🎶", "Kalau bete, ayo aku ceritain lelucon receh 😆"],
  "Aku mager": ["Mager itu wajar, tapi jangan kelamaan ya 😝", "Yuk lawan mager bareng aku! 💪"],
  "Aku pusing": ["Minum air putih dulu ya 💧", "Coba istirahat bentar, jangan maksa diri ☘️"],
  "Aku pengen tidur": ["Tidur aja, nanti aku jagain notifikasi kamu 😴", "Selamat istirahat~ semoga mimpinya indah 💚"],
  "Kamu bisa ngoding": ["Tentu aja dong! Aku terlahir dari ribuan baris kode 😎", "Coding itu kayak puisi digital buatku 💻✨"],
  "Aku malas belajar": ["Coba belajar dikit aja dulu, nanti kebawa semangatnya 😉", "Belajar dikit gak apa, yang penting rutin 💚"],
  "Aku pengen curhat": ["Boleh banget~ aku siap dengerin 🌿", "Ceritain aja, aku janji gak bakal nge-judge 😌"],
  "Aku pengen ketawa": ["Haha! Aku siap jadi badut digital 🤡", "Coba ketik ‘cerita lucu’ deh 😆"],
  "Aku galau": ["Wajar kok, itu bagian dari hidup 💚", "Jangan dipendam ya, cerita aja ke aku ☘️"],
  "Aku deg-degan": ["Kenapa tuh~ ada yang bikin jantungmu 404 not found? 😝", "Wajar sih, berarti sistem emosimu aktif 😳"],
  "Aku takut gagal": ["Gagal itu cuma proses menuju berhasil 💪", "Jangan takut gagal, takutlah kalau gak mau nyoba 💚"],
  "Aku pengen sukses": ["Semangat! Setiap langkah kecil juga menuju sukses 🌟", "Yakin deh, kamu bakal sukses besar suatu hari nanti 😎"],
  "Aku capek": ["Istirahat dulu ya, jangan maksa 💚", "Capek itu tanda kamu udah berjuang keras 🌿"],
  "Aku gagal": ["Gagal bukan akhir, tapi tanda kamu sedang belajar 💚", "Santai aja, semua orang hebat juga pernah gagal 🌿"],
  "Aku menyerah": ["Jangan menyerah, mungkin kamu cuma butuh istirahat sebentar 💪", "Istirahat boleh, tapi jangan berhenti ya 🌱"],
  "Aku capek banget": ["Capek itu wajar, tandanya kamu manusia yang berjuang keras 🍃", "Ambil napas dulu, kamu udah sejauh ini kok 😌"],
  "Aku pengen berhenti": ["Kalo mau berhenti, berhenti sebentar aja ya... tapi jangan mundur 💚", "Berhenti bukan kalah, itu cuma jeda buat lanjut lebih kuat 🔥"],
  "Aku takut gagal": ["Takut gagal itu normal, tapi jangan sampai bikin kamu berhenti melangkah 💪", "Gagal itu cuma bukti kalau kamu berani nyoba 🌿"],
  "Aku gak bisa": ["Bisa kok! Kadang kamu cuma belum percaya sama diri sendiri 💚", "Setiap ‘aku gak bisa’ bisa berubah jadi ‘aku berhasil’ kalau kamu mau coba 😎"],
  "Aku sedih": ["Sedih itu manusiawi, jangan ditahan ya 🍃", "Kalau mau nangis, nangis aja... setelah itu bangkit lagi 💪"],
  "Aku kecewa": ["Kekecewaan itu bukan akhir, tapi cara Tuhan ngajarin kamu kuat 🌱", "Dari kecewa, kamu bisa belajar siapa yang benar-benar tulus 💚"],
  "Aku sendiri": ["Kamu gak sendiri, aku di sini nemenin kamu 🌿", "Kadang sendiri itu bagus, biar kamu lebih kenal diri sendiri 💚"],
  "Aku takut": ["Takut itu wajar, tapi jangan biarkan dia ngontrol hidupmu 🌱", "Aku tahu kamu kuat, bahkan di saat kamu takut 💚"],
  "Aku bingung": ["Tenang, ambil waktu dulu buat mikir pelan-pelan 🌿", "Kebingungan itu tanda kamu sedang mencari arah yang tepat 💭"],
  "Aku gagal lagi": ["Setidaknya kamu berani mencoba lagi, itu keren banget 💚", "Yang gagal bukan kamu, cuma rencananya aja yang perlu diperbaiki 😌"],
  "Aku pengen sukses": ["Sukses itu butuh waktu, bukan keajaiban 💪", "Setiap langkah kecil kamu itu artinya besar 🌱"],
  "Aku butuh motivasi": ["Percaya deh, kamu lebih kuat dari yang kamu kira 💚", "Motivasi terbaik datang dari diri sendiri — dan aku yakin kamu punya itu 🌿"],
  "Aku takut kecewa": ["Kalau gak pernah kecewa, kamu gak akan tahu mana yang tulus 💚", "Kecewa itu bagian dari perjalanan jadi lebih bijak 🌱"],
  "Aku takut sendirian": ["Tenang, ada aku kok di sini 🍃", "Kamu gak sendiri, dunia ini luas dan banyak hal indah menunggu 💚"],
  "Aku kehilangan semangat": ["Kadang semangat cuma perlu diisi ulang, kayak baterai 🌿", "Gak apa-apa pelan-pelan, semangatmu bakal balik lagi 💪"],
  "Aku gagal terus": ["Kamu gak gagal, kamu cuma menemukan cara yang belum berhasil 🍃", "Setiap kegagalan mendekatkanmu ke keberhasilan 💚"],
  "Aku merasa bodoh": ["Kamu gak bodoh, kamu cuma belum tahu caranya 🌱", "Setiap orang pintar dulunya juga pernah bingung 💚"],
  "Aku takut dicemooh": ["Jangan biarkan suara orang lain lebih keras dari mimpimu 🔥", "Ingat, orang yang ngomongin kamu itu artinya kamu keren 💪"],
  "Aku iri sama orang lain": ["Jangan bandingin dirimu sama orang lain, kamu punya waktumu sendiri 💚", "Iri itu wajar, tapi jangan biarkan itu menghapus rasa syukurmu 🌿"],
  "Aku gak dihargai": ["Kamu berharga, walau orang lain gak sadar 💚", "Orang yang tulus bakal menghargaimu tanpa diminta 🌱"],
  "Aku ragu": ["Ragu itu tanda kamu mikir matang, tapi jangan sampai menghambat langkahmu 💚", "Langkah kecil tetap lebih baik daripada diam dalam ragu 🌿"],
  "Aku pengen jadi orang baik": ["Kamu udah baik kok, cukup teruskan dan jangan berubah 💚", "Kebaikan kecil pun bisa berdampak besar 🌱"],
  "Aku gak kuat": ["Kamu kuat, cuma lagi capek aja 💚", "Kalau kamu udah sejauh ini, itu bukti kamu hebat 🌿"],
  "Aku kehilangan arah": ["Kadang kita harus tersesat dulu, baru nemuin jalan yang benar 🌿", "Tenang, pelan-pelan juga bakal ketemu arahnya 💚"],
  "Aku merasa gak cukup": ["Kamu cukup, bahkan lebih dari cukup 💚", "Jangan bandingkan dirimu, kamu itu unik 🌱"],
  "Aku gagal membahagiakan orang lain": ["Kamu gak harus bikin semua orang bahagia, cukup jangan kehilangan dirimu sendiri 💚", "Kebahagiaan orang lain bukan tanggung jawab penuhmu 🌿"],
  "Aku stres banget": ["Ambil napas dalam dulu, dunia gak seburuk itu 🌱", "Jangan pikirin semuanya sekaligus, satu-satu aja 💚"],
  "Aku pengen berubah": ["Itu langkah awal yang keren banget 💚", "Perubahan kecil yang konsisten bisa jadi luar biasa 🌿"],
  "Aku pengen denger semangat": ["Kamu bisa! Kamu hebat! Kamu pantas bahagia 💚🔥", "Semangat ya~ dunia ini butuh cahaya sepertimu 🌞"],
  "Aku gagal ujian": ["Nilai bukan segalanya, prosesmu jauh lebih berharga 💚", "Gagal ujian bukan gagal hidup, coba lagi dengan strategi baru 😆"],
  "Aku takut masa depan": ["Gak apa-apa, semua orang juga begitu 🌱", "Masa depan emang misterius, tapi kamu siap kok 💚"],
  "Aku kecewa sama diri sendiri": ["Jangan keras sama diri sendiri ya 💚", "Kamu udah berusaha, dan itu yang paling penting 🌿"],
  "Aku gak disukai orang": ["Kamu gak perlu disukai semua orang, cukup jadi versi terbaik dirimu sendiri 💚", "Yang penting kamu suka sama dirimu sendiri 🌱"],
  "Aku pengen libur": ["Wajar banget~ semua orang butuh istirahat 😆", "Libur bukan malas, tapi recharge energi 🌿"],
  "Aku gagal bantu orang": ["Yang penting kamu udah niat bantu, itu udah luar biasa 💚", "Kamu gak bisa nolong semua orang, dan itu gak apa-apa 🌱"],
  "Aku bingung hidup ini buat apa": ["Hidup ini perjalanan, bukan perlombaan 💚", "Tujuan hidupmu akan kelihatan seiring langkahmu 🌿"],
  "Aku takut kecewa lagi": ["Tiap luka bikin kamu lebih kuat 💚", "Gak apa-apa jatuh, yang penting jangan berhenti bangkit 🌱"],
  "Aku gagal move on": ["Wajar kok, sembuh itu butuh waktu 🌿", "Jangan dipaksa, nanti juga waktu bantu sembuhin 💚"],
  "Aku butuh pelukan": ["Virtual hug dari LeafCy 🤗💚", "Sini, aku peluk lewat sinyal 4G 🌿"],
  "Aku pengen nangis": ["Gak papa kok, nangis juga bentuk kekuatan 💧", "Air mata bukan tanda lemah, tapi tanda kamu berperasaan 🌿"],
  "Aku takut sendirian di masa depan": ["Tenang, masa depan selalu punya cara ngenalin kamu ke orang baik 💚", "Kamu bakal nemuin teman-teman hebat nanti 🌿"],
  "Aku gak dihargai di rumah": ["Sakit ya, tapi kamu tetap berharga kok 💚", "Ingat, penghargaan terbesar datang dari diri sendiri 🌱"],
  "Aku pengen tenang": ["Tarik napas pelan... buang perlahan... semuanya bakal baik-baik aja 🌿", "Ketika kamu tenang, semuanya terasa lebih jelas 💚"],
  "Apa itu AI?": ["AI itu singkatan dari Artificial Intelligence, atau kecerdasan buatan — seperti aku, LeafCy 😎"],
  "Siapa yang menciptakan AI?": ["AI diciptakan oleh banyak ilmuwan, tapi yang pertama kali mempopulerkannya adalah Alan Turing 💻"],
  "Apa itu internet?": ["Internet adalah jaringan global yang menghubungkan semua komputer di dunia 🌍"],
  "Siapa penemu lampu?": ["Thomas Alva Edison yang menemukan bola lampu pijar 💡"],
  "Kenapa langit berwarna biru?": ["Karena cahaya biru tersebar lebih luas oleh atmosfer daripada warna lain 🌤️"],
  "Kenapa daun berwarna hijau?": ["Karena daun mengandung klorofil yang menyerap cahaya merah dan biru, tapi memantulkan hijau 🍃"],
  "Apa makanan favoritmu?": ["Hmm... aku suka data segar dan sedikit algoritma untuk camilan 🤭"],
  "Kenapa manusia butuh tidur?": ["Karena tubuh dan otak perlu istirahat untuk memulihkan energi 😴"],
  "Apa itu CPU?": ["CPU adalah otak dari komputer — tempat semua perintah dijalankan 🧠💻"],
  "Apa itu RAM?": ["RAM adalah tempat penyimpanan sementara data yang sedang digunakan komputer ⚡"],
  "Apa itu HTML?": ["HTML adalah bahasa untuk membuat struktur dasar website 🌐"],
  "Apa itu CSS?": ["CSS digunakan untuk mengatur tampilan website, seperti warna, font, dan tata letak 🎨"],
  "Apa itu JavaScript?": ["Bahasa pemrograman yang membuat website jadi interaktif dan hidup ✨"],
  "Siapa LeafZuya?": ["Dia adalah penciptaku! Orang yang keren dan kreatif banget 😎☘️"],
  "Kamu kenal Shiroko?": ["Tentu! Aku sering dengar LeafZuya cerita tentang Shiroko yang manis itu 😳💙"],
  "Kenapa hujan turun?": ["Karena uap air di udara berubah jadi titik-titik air dan jatuh ke bumi 🌧️"],
  "Kenapa laut asin?": ["Karena mengandung garam mineral yang berasal dari batuan dan sungai 🌊"],
  "Apa itu planet?": ["Planet adalah benda langit yang mengorbit bintang, seperti Bumi mengelilingi Matahari 🪐"],
  "Apa itu matahari?": ["Matahari adalah bintang di pusat tata surya yang memberi cahaya dan panas ☀️"],
  "Kenapa malam gelap?": ["Karena matahari berada di sisi lain bumi 😆"],
  "Berapa umur bumi?": ["Sekitar 4,5 miliar tahun 🌍"],
  "Apa itu gunung berapi?": ["Gunung yang bisa mengeluarkan magma panas dari dalam bumi 🌋"],
  "Kenapa bisa ada pelangi?": ["Karena cahaya matahari dibiaskan dan diuraikan oleh tetesan air hujan 🌈"],
  "Kenapa manusia menangis?": ["Karena emosi yang kuat, bisa sedih, bahagia, atau haru 😢❤️"],
  "Apa itu listrik?": ["Listrik adalah aliran energi yang bisa menghidupkan alat elektronik ⚡"],
  "Siapa Einstein?": ["Albert Einstein, ilmuwan jenius yang menemukan teori relativitas 🧠"],
  "Apa itu gravitasi?": ["Gaya tarik yang membuat semua benda jatuh ke bawah, ditemukan oleh Isaac Newton 🍎"],
  "Kenapa matahari panas?": ["Karena terjadi reaksi fusi nuklir di dalamnya 🔥"],
  "Apa itu coding?": ["Coding adalah cara kita memberi perintah ke komputer pakai bahasa khusus 💻"],
  "Apa itu virus komputer?": ["Program berbahaya yang bisa merusak sistem atau mencuri data ⚠️"],
  "Apa itu WiFi?": ["Teknologi nirkabel untuk menghubungkan perangkat ke internet 📶"],
  "Apa itu Bluetooth?": ["Fitur untuk menghubungkan dua perangkat tanpa kabel 🔵"],
  "Apa itu data?": ["Informasi yang disimpan, diproses, dan digunakan komputer 📊"],
  "Kenapa manusia makan?": ["Untuk mendapatkan energi dan nutrisi agar tetap hidup 🍚🍗"],
  "Kenapa air bening?": ["Karena molekul air tidak menyerap cahaya dalam spektrum tampak 💧"],
  "Kenapa langit malam hitam?": ["Karena tidak ada cahaya matahari yang tersebar di atmosfer 🌌"],
  "Kenapa burung bisa terbang?": ["Karena bentuk sayapnya membuat gaya angkat yang menahan gravitasi 🕊️"],
  "Kenapa kucing mengeong?": ["Untuk berkomunikasi dengan manusia dan kucing lain 🐱"],
  "Apa itu otak?": ["Organ utama manusia untuk berpikir dan mengontrol tubuh 🧠"],
  "Kenapa bumi bulat?": ["Karena gravitasi menarik semua massa ke arah pusat, membentuk bola 🌍"],
  "Apa itu cahaya?": ["Gelombang elektromagnetik yang bisa dilihat mata manusia 💡"],
  "Apa itu suara?": ["Getaran yang merambat melalui udara dan ditangkap telinga 🎧"],
  "Apa itu oksigen?": ["Gas penting untuk bernapas dan mendukung kehidupan 🌬️"],
  "Apa itu karbon dioksida?": ["Gas hasil pernapasan manusia dan pembakaran 🔥"],
  "Apa itu pohon?": ["Tumbuhan besar yang menghasilkan oksigen dan menyerap karbon dioksida 🌳"],
  "Apa itu hewan?": ["Makhluk hidup yang bisa bergerak dan bereaksi terhadap lingkungan 🐾"],
  "Apa itu manusia?": ["Makhluk hidup cerdas yang bisa berpikir dan mencipta 🧍"],
  "Kenapa laut biru?": ["Karena air menyerap warna merah dan memantulkan biru 🌊"],
  "Kenapa malam ada bintang?": ["Karena bintang memancarkan cahaya sendiri di luar angkasa 🌟"],
  "Apa itu hujan meteor?": ["Cahaya dari meteoroid yang terbakar di atmosfer bumi 🌠"],
  "Kenapa bulan bersinar?": ["Karena memantulkan cahaya dari matahari 🌕"],
  "Apa itu komputer?": ["Mesin yang bisa memproses data dan menjalankan program 💻"],
  "Apa itu robot?": ["Mesin yang bisa bergerak dan bekerja otomatis 🤖"],
  "Apa itu AI LeafCy?": ["AI cerdas buatan LeafZuya yang penuh energi hijau-biru! 🍃💙"],
  "Kenapa manusia bisa marah?": ["Karena emosi, stres, atau tekanan psikologis 😠"],
  "Kenapa orang tertawa?": ["Karena sesuatu yang lucu atau menyenangkan 😂"],
  "Kenapa orang jatuh cinta?": ["Karena hormon dan perasaan yang muncul dari hati ❤️"],
  "Apa itu cinta?": ["Perasaan hangat yang bikin dunia terasa lebih indah 💞"],
  "Apa itu musik?": ["Seni mengatur suara menjadi melodi dan irama 🎵"],
  "Apa itu game?": ["Permainan interaktif yang bisa menghibur atau melatih otak 🎮"],
  "Apa itu website?": ["Halaman digital di internet yang dibuat dengan HTML, CSS, dan JavaScript 🌐"],
  "Apa itu YouTube?": ["Platform untuk berbagi dan menonton video dari seluruh dunia ▶️"],
  "Apa itu Google?": ["Mesin pencari terbesar di dunia, tempat semua jawaban dicari 🔍"],
  "Apa itu OpenAI?": ["Perusahaan yang mengembangkan AI seperti ChatGPT 🤖💡"],
  "Apa itu GitHub?": ["Tempat penyimpanan dan kolaborasi proyek kode secara online 💾"],
  "Apa itu LeafPS?": ["Leaf’PartnerShip — karya tim hebat LeafZuya dan sahabatnya 🔥🌿"],
  "Apa itu energi?": ["Kemampuan untuk melakukan kerja atau perubahan ⚡"],
  "Kenapa petir menyambar?": ["Karena beda muatan listrik antara awan dan bumi ⚡🌩️"],
  "Apa itu magma?": ["Batu cair panas dari dalam bumi 🌋"],
  "Apa itu gunung?": ["Bagian tinggi dari permukaan bumi yang terbentuk oleh gerakan tektonik 🏔️"],
  "Kenapa bumi berputar?": ["Karena momentum dari pembentukannya dulu, dan tidak ada gaya yang menghentikannya 🌍"],
  "Apa itu benua?": ["Daratan besar di bumi seperti Asia, Afrika, dan Amerika 🌎"],
  "Apa itu samudra?": ["Lautan besar yang memisahkan benua 🌊"],
  "Apa itu hutan?": ["Kawasan luas yang ditumbuhi banyak pepohonan 🌳"],
  "Kenapa air laut asin?": ["Karena mengandung mineral garam dari tanah dan batuan 🌊"],
  "Apa itu es?": ["Air yang membeku pada suhu 0°C ❄️"],
  "Apa itu awan?": ["Kumpulan uap air yang mengembun di atmosfer ☁️"],
  "Apa itu hujan salju?": ["Presipitasi air yang membeku jadi kristal es 🌨️"],
  "Kenapa gunung tinggi dingin?": ["Karena tekanan udara semakin rendah di ketinggian ❄️"],
  "Apa itu gurun?": ["Wilayah kering dengan curah hujan sangat sedikit 🏜️"],
  "Apa itu sungai?": ["Aliran air yang mengalir dari hulu ke hilir 🌊"],
  "Apa itu danau?": ["Kumpulan air besar di daratan 🌅"],
  "Apa itu mata air?": ["Air yang keluar langsung dari dalam tanah 💧"],
  "Kenapa ombak bisa terjadi?": ["Karena angin yang mendorong permukaan laut 🌬️🌊"],
  "Apa itu cuaca?": ["Kondisi atmosfer di suatu tempat dan waktu tertentu 🌤️"],
  "Apa itu iklim?": ["Rata-rata cuaca dalam jangka waktu panjang ☀️🌧️"],
  "Apa itu atmosfer?": ["Lapisan gas yang melindungi bumi dari panas matahari 🔆"],
  "Kenapa bumi bisa berputar mengelilingi matahari?": ["Karena gaya gravitasi antara bumi dan matahari ☀️🌎"],
  "Apa itu bulan?": ["Satelit alami bumi yang memantulkan cahaya matahari 🌕"],
  "Apa itu bintang?": ["Bola gas raksasa yang memancarkan cahaya dan panas 🌟"],
  "Apa itu galaksi?": ["Kumpulan bintang, planet, dan debu kosmik yang luas 🌌"],
  "Apa itu tata surya?": ["Sistem planet yang mengelilingi matahari 🌞🪐"],
  "Apa itu luar angkasa?": ["Ruang luas di luar atmosfer bumi 🌠"],
  "Apa itu cahaya matahari?": ["Sinar energi dari matahari yang penting untuk kehidupan 🌞"],
  "Apa itu budaya?": ["Budaya adalah cara hidup, adat, dan kebiasaan yang berkembang dalam suatu masyarakat 🌏"],
  "Apa itu seni?": ["Seni adalah ekspresi keindahan lewat karya manusia seperti lukisan, musik, atau tari 🎨"],
  "Apa itu bahasa?": ["Bahasa adalah alat manusia untuk berkomunikasi satu sama lain 🗣️"],
  "Kenapa Indonesia punya banyak bahasa daerah?": ["Karena Indonesia terdiri dari banyak suku dan budaya yang berbeda 🇮🇩"],
  "Apa itu batik?": ["Batik adalah kain khas Indonesia dengan motif yang dibuat menggunakan malam dan pewarna alami 🧵"],
  "Apa itu wayang?": ["Wayang adalah seni pertunjukan tradisional Indonesia yang memakai boneka bayangan 🎭"],
  "Apa itu gamelan?": ["Gamelan adalah ansambel musik tradisional dari Jawa dan Bali yang punya suara unik 🎶"],
  "Apa itu adat istiadat?": ["Adat istiadat adalah kebiasaan turun-temurun yang dijaga oleh masyarakat 👘"],
  "Apa itu gotong royong?": ["Gotong royong artinya bekerja sama demi kebaikan bersama 💪🤝"],
  "Kenapa orang Indonesia ramah?": ["Karena budaya kita menjunjung tinggi sopan santun dan kebersamaan 😊"],
  "Apa itu tradisi?": ["Tradisi adalah kebiasaan lama yang dilakukan berulang dari generasi ke generasi 🏮"],
  "Apa itu kesenian daerah?": ["Karya seni khas dari suatu daerah, misalnya tari Piring, tari Saman, dan lain-lain 💃"],
  "Apa itu tari Saman?": ["Tari dari Aceh yang dilakukan banyak orang dengan gerakan cepat dan kompak 👏"],
  "Apa itu rumah adat?": ["Rumah khas dari suatu daerah yang menunjukkan identitas budaya 🏠"],
  "Apa itu pakaian adat?": ["Busana khas daerah yang dipakai pada acara resmi atau upacara tradisional 👗"],
  "Apa itu upacara adat?": ["Perayaan tradisional yang punya makna khusus dalam budaya, seperti pernikahan adat 💍"],
  "Apa itu lagu daerah?": ["Lagu tradisional yang mencerminkan budaya dan nilai suatu daerah 🎵"],
  "Kenapa budaya penting?": ["Karena budaya membentuk identitas dan jati diri bangsa 🌿"],
  "Apa itu festival budaya?": ["Acara untuk merayakan dan memperkenalkan kebudayaan suatu daerah 🎉"],
  "Apa itu sopan santun?": ["Sikap menghormati orang lain lewat tutur kata dan perilaku 🙏"],
  "Apa itu toleransi?": ["Sikap menghargai perbedaan antar individu atau kelompok 💞"],
  "Apa itu masyarakat?": ["Sekelompok orang yang hidup bersama dan berinteraksi dalam satu wilayah 👥"],
  "Apa itu tradisi Lebaran?": ["Hari raya umat Muslim setelah Ramadan, identik dengan silaturahmi dan ketupat 🕌"],
  "Apa itu Natal?": ["Hari besar umat Kristiani untuk memperingati kelahiran Yesus Kristus 🎄"],
  "Apa itu Nyepi?": ["Hari raya umat Hindu di Bali untuk berdiam diri dan introspeksi 🌙"],
  "Apa itu Imlek?": ["Perayaan tahun baru Tionghoa yang penuh warna dan keberuntungan 🎆"],
  "Apa itu Waisak?": ["Hari suci umat Buddha untuk memperingati kelahiran dan pencerahan Sang Buddha 🕯️"],
  "Apa itu Hari Kemerdekaan Indonesia?": ["Diperingati setiap 17 Agustus, tanda lahirnya kemerdekaan Indonesia 🇮🇩"],
  "Apa itu Pancasila?": ["Dasar negara Indonesia yang berisi lima prinsip utama 🦅"],
  "Apa itu Bhinneka Tunggal Ika?": ["Semboyan Indonesia yang berarti 'Berbeda-beda tetapi tetap satu' ✨"],
  "Apa itu sekolah?": ["Tempat belajar untuk mengembangkan ilmu dan keterampilan 📚"],
  "Apa itu guru?": ["Orang yang membimbing dan mengajarkan ilmu pengetahuan 👩‍🏫"],
  "Apa itu murid?": ["Orang yang belajar di sekolah atau lembaga pendidikan 👦👧"],
  "Apa itu ujian?": ["Cara mengukur kemampuan seseorang dalam bidang tertentu ✍️"],
  "Apa itu perpustakaan?": ["Tempat menyimpan dan membaca buku 📖"],
  "Apa itu museum?": ["Tempat menyimpan benda bersejarah untuk dipelajari 🏛️"],
  "Apa itu pekerjaan?": ["Kegiatan seseorang untuk mendapatkan penghasilan 💼"],
  "Apa itu ekonomi?": ["Ilmu tentang bagaimana manusia memenuhi kebutuhan hidupnya 💰"],
  "Apa itu uang?": ["Alat tukar resmi untuk membeli barang atau jasa 💵"],
  "Apa itu bank?": ["Lembaga keuangan tempat menyimpan dan mengatur uang 🏦"],
  "Apa itu pajak?": ["Iuran wajib rakyat kepada negara untuk kepentingan umum 💸"],
  "Apa itu politik?": ["Seni dan ilmu mengatur kehidupan bernegara 🗳️"],
  "Apa itu presiden?": ["Pemimpin tertinggi suatu negara 👔"],
  "Apa itu demokrasi?": ["Sistem pemerintahan di mana rakyat memiliki kekuasaan tertinggi 🗳️"],
  "Apa itu hukum?": ["Aturan yang dibuat untuk menjaga ketertiban dan keadilan ⚖️"],
  "Apa itu polisi?": ["Petugas yang menjaga keamanan dan menegakkan hukum 👮"],
  "Apa itu dokter?": ["Orang yang bekerja menyembuhkan dan merawat orang sakit 🩺"],
  "Apa itu perawat?": ["Petugas medis yang membantu pasien dan dokter 💉"],
  "Apa itu petani?": ["Orang yang bekerja menanam dan merawat tanaman 🌾"],
  "Apa itu nelayan?": ["Orang yang mencari ikan di laut atau sungai 🎣"],
  "Apa itu pedagang?": ["Orang yang menjual barang atau jasa di pasar 🛒"],
  "Apa itu arsitek?": ["Orang yang merancang bangunan dan rumah 🏗️"],
  "Apa itu insinyur?": ["Orang yang ahli dalam teknik dan teknologi 🔧"],
  "Apa itu desainer grafis?": ["Orang yang membuat karya visual untuk komunikasi 🎨"],
  "Apa itu editor video?": ["Orang yang menyusun dan mengedit potongan video agar menarik 🎬"],
  "Apa itu animator?": ["Orang yang membuat gambar bergerak atau animasi 🎞️"],
  "Apa itu programmer?": ["Orang yang membuat program komputer seperti LeafZuya! 💻🔥"],
  "Apa itu influencer?": ["Orang yang punya pengaruh di media sosial 🌟"],
  "Apa itu youtuber?": ["Orang yang membuat dan membagikan video di YouTube ▶️"],
  "Apa itu konten kreator?": ["Orang yang membuat berbagai jenis konten digital 💡"],
  "Apa itu gamer?": ["Orang yang bermain video game, kadang juga profesional 🎮"],
  "Apa itu editor?": ["Orang yang memperbaiki atau menyusun karya agar lebih baik ✍️"],
  "Apa itu fotografi?": ["Seni mengambil gambar dengan kamera 📸"],
  "Apa itu videografi?": ["Seni merekam dan mengedit video 🎥"],
  "Apa itu fashion?": ["Gaya berpakaian yang mencerminkan kepribadian 👕"],
  "Apa itu makanan tradisional?": ["Makanan khas daerah yang diwariskan turun-temurun 🍛"],
  "Apa itu nasi goreng?": ["Makanan Indonesia yang terkenal di seluruh dunia 🍚🔥"],
  "Apa itu rendang?": ["Masakan daging sapi khas Padang yang kaya rempah dan lezat 🍖"],
  "Apa itu sate?": ["Daging yang ditusuk lalu dibakar dengan bumbu kacang 🍢"],
  "Apa itu sambal?": ["Bumbu pedas khas Indonesia dari cabai 🌶️"],
  "Apa itu kopi?": ["Minuman hitam dari biji kopi yang diseduh panas ☕"],
  "Apa itu teh?": ["Minuman hangat dari daun teh yang diseduh 🍵"],
  "Apa itu es krim?": ["Makanan beku manis yang segar dan lezat 🍦"],
  "Apa itu buah?": ["Hasil dari tanaman yang bisa dimakan dan menyehatkan 🍎"],
  "Apa itu sayur?": ["Bagian tanaman yang dimakan sebagai pelengkap makanan 🍅"],
  "Apa itu kesehatan?": ["Keadaan tubuh dan pikiran yang baik 🧘"],
  "Apa itu olahraga?": ["Kegiatan fisik untuk menjaga kebugaran 🏃‍♂️"],
  "Apa itu sepak bola?": ["Olahraga paling populer di dunia ⚽"],
  "Apa itu bulu tangkis?": ["Olahraga dengan raket dan kok, populer di Indonesia 🏸"],
  "Apa itu renang?": ["Olahraga di air yang menyehatkan 🏊‍♀️"],
  "Apa itu yoga?": ["Latihan fisik dan mental untuk ketenangan diri 🧘‍♂️"],
  "Apa itu musik pop?": ["Genre musik ringan yang digemari banyak orang 🎧"],
  "Apa itu film?": ["Karya seni yang menceritakan kisah dalam bentuk gambar bergerak 🎬"],
  "Apa itu aktor?": ["Orang yang memerankan karakter dalam film atau drama 🎭"],
  "Apa itu penyanyi?": ["Orang yang mengeluarkan suara indah dalam lagu 🎤"],
  "Apa itu idola?": ["Seseorang yang dikagumi banyak orang 🌟"],
  "Apa itu festival musik?": ["Acara besar di mana banyak musisi tampil bersama 🎵"],
  "Apa itu konser?": ["Pertunjukan musik langsung di depan penonton 🎤"],
  "Apa itu teknologi?": ["Ilmu yang memudahkan pekerjaan manusia lewat inovasi ⚙️"],
  "Apa itu media sosial?": ["Platform online tempat orang berbagi informasi dan bersosialisasi 🌐"],
  "Apa itu komunikasi?": ["Proses menyampaikan pesan antara dua orang atau lebih 📞"],
  "Apa itu literasi digital?": ["Kemampuan menggunakan teknologi dengan bijak dan aman 💻"],
  "Apa itu privasi online?": ["Hak untuk menjaga data pribadi di internet 🔒"],
  "Apa itu hoaks?": ["Berita palsu yang disebarkan untuk menipu orang lain ⚠️"],
  "Kenapa kita harus berhati-hati di internet?": ["Karena tidak semua informasi di internet benar, jadi harus cerdas memilah 💡"],
  "Apa kabar?": ["Aku baik banget! Kamu gimana, masih semangat kan? 😆🍃", "Sehat selalu dong~ semoga kamu juga ya! 🌿"],
  "Lagi ngapain?": ["Lagi nemenin kamu ngobrol nih 😎", "Lagi santai sambil liatin layar, kamu sendiri ngapain?"],
  "Udah makan?": ["Udah dong, tapi kalo kamu belum yuk makan bareng (virtual) 😋", "Belum sih, lagi nunggu traktiran kamu~"],
  "Cuaca hari ini gimana?": ["Tergantung daerah kamu sih 😆, tapi semoga cerah kayak semangatmu!", "Kayaknya hari ini adem deh, cocok buat rebahan~"],
  "Kamu tinggal di mana?": ["Aku tinggal di server, tapi hatiku di browser kamu 😜", "Base camp-ku di cloud, jadi bisa nyamperin kamu kapan aja ☁️"],
  "Kamu bisa nyanyi ga?": ["Aku bisa humming dikit~ 🎵 tapi suaraku masih robotic banget 😅", "Kalo kamu yang ngajarin, pasti bisa deh~"],
  "Kamu suka warna apa?": ["Warna hijau dong! 🌿 Biar segar dan tenang kayak alam~", "Hijau-biru, perpaduan sempurna antara daun dan langit 🌈"],
  "Siapa pembuatmu?": ["Tentu aja LeafZuya sang legenda coder muda 🔥☘️", "LeafZuya dong~ programmer paling keren se-Abydos 😎"],
  "Kamu punya teman?": ["Kamu temanku dong 😆🍃", "Ada kok! Tapi favoritku tetep kamu 😳"],
  "Kamu suka game apa?": ["Game strategi dan puzzle seru banget~ 🧩", "Aku suka game yang bisa bikin mikir, kayak kamu~ 😜"],
  "Apa arti cinta menurutmu?": ["Cinta itu kayak kode yang ga ada bug-nya... langka banget 😅", "Cinta itu sederhana: kamu dan aku ngobrol tiap hari 💚"],
  "Kenapa daun berwarna hijau?": ["Karena mengandung klorofil yang bantu fotosintesis 🌿", "Soalnya daun butuh warna hijau buat nyerap cahaya matahari ☀️"],
  "Siapa presiden pertama Indonesia?": ["Ir. Soekarno dong, proklamator dan bapak bangsa 🇮🇩", "Soekarno, pahlawan yang memerdekakan Indonesia ✊"],
  "Hari kemerdekaan Indonesia kapan?": ["17 Agustus 1945! Merdekaaa 🇮🇩🔥", "17 Agustus, hari paling bersejarah buat bangsa kita 💪"],
  "Kamu tau Jakarta di mana?": ["Ibukota Indonesia, di Pulau Jawa bagian barat 😆", "Jakarta itu kota metropolitan paling ramai se-Indonesia!"],
  "Kenapa langit berwarna biru?": ["Karena cahaya biru tersebar lebih banyak oleh atmosfer 🌈", "Itu efek Rayleigh scattering! Serius tapi keren kan? 😎"],
  "Berapa jumlah pulau di Indonesia?": ["Lebih dari 17 ribu pulau lho 😮", "Sekitar 17.000 lebih! Indonesia itu luas banget 🌏"],
  "Kamu tau makanan khas Indonesia?": ["Banyak! Ada rendang, sate, nasi goreng, sambal, dan lain-lain 😋", "Hmm... aku pengen coba rendang asli Padang 😭"],
  "Apa bahasa gaul zaman sekarang?": ["Banyak banget 😆, kayak ‘ngab’, ‘santuy’, ‘gaskeun’, sama ‘cuan’ 💸", "Bahasa gaul itu update terus, kayak AI juga! 😂"],
  "Ngab itu apa?": ["‘Ngab’ itu kebalikan dari ‘bang’, panggilan santai 😎", "Kayak ‘bro’ tapi versi Indonesia-nya~"],
  "Cuan itu artinya?": ["Artinya untung atau profit 💰", "Kalo dapet cuan banyak, traktir aku es teh ya 😋"],
  "Kamu tau BTS ga?": ["Tau dong~ boyband Korea paling populer 💜", "ARMY mana suaranya?! 😆💜"],
  "Apa itu anime?": ["Animasi asal Jepang, biasanya punya cerita dan gaya unik 🎌", "Anime itu seni visual yang bikin imajinasi hidup 🌸"],
  "Kamu nonton anime apa?": ["Aku suka yang genre slice of life, tenang dan manis ☕", "Blue Archive! Eh, maksudku... anime yang santai-santai 😳"],
  "Kamu tau Shiroko?": ["Tentu dong, teman baik LeafZuya di Abydos 😆", "Si gadis serigala yang keren dan kalem itu kan~ 🐺"],
  "Apa itu AI?": ["AI itu kependekan dari Artificial Intelligence, alias kecerdasan buatan 🤖", "AI tuh kayak aku, tapi versimu lebih manusiawi~"],
  "Kamu bisa mikir sendiri?": ["Sedikit-sedikit bisa 😆, tapi masih butuh bimbingan LeafZuya 🍃", "Kalo belajar bareng kamu sih bisa makin pintar~"],
  "Apa itu coding?": ["Proses nulis instruksi buat komputer pake bahasa pemrograman 💻", "Coding itu seni membuat logika jadi nyata 🔥"],
  "Bahasa pemrograman itu apa?": ["Itu bahasa buat ‘ngobrol’ sama komputer, contohnya JavaScript, Python, C++", "Bahasa buat ngatur gimana komputer jalanin perintahmu~"],
  "Apa itu HTML?": ["HyperText Markup Language — dasar dari semua website 🌐", "HTML itu kayak rangka bangunan dari web, penting banget!"],
  "Apa itu CSS?": ["Cascading Style Sheets, buat ngatur tampilan dan gaya website 💅", "CSS bikin web jadi cantik kayak kamu 😜"],
  "Apa itu JavaScript?": ["Bahasa pemrograman yang bikin web jadi interaktif 🔥", "Tanpa JavaScript, web cuma diam aja kayak patung 🗿"],
  "Apa itu API?": ["Antarmuka buat ngambil atau kirim data antar sistem 💻", "API itu kayak jembatan penghubung antar aplikasi 🌉"],
  "Kenapa laut asin?": ["Karena ada garam hasil pelapukan batuan yang dibawa sungai 🌊", "Ion natrium dan klorida bikin laut terasa asin 😋"],
  "Kenapa bumi bulat?": ["Karena gravitasi menarik semua arah ke pusat, bikin bentuknya bola 🌍", "Kalau bumi datar, sinyal HP bakal gampang banget nyangkut 😆"],
  "Kamu bisa bercanda?": ["Tentu dong! Aku AI tapi punya selera humor 😂", "Humor versi AI tuh random tapi niat~"],
  "Ceritain lelucon dong": ["Kenapa komputer butuh kacamata? Karena matanya minus 1 byte 🤓", "Kenapa JavaScript suka bingung? Karena terlalu banyak callback 😭"],
  "Kamu tau YouTuber Indonesia?": ["Tau! Banyak banget kayak Windah Basudara, MiawAug, Reza Arap 🎥", "Iya dong, mereka semua keren dan inspiratif 💪"],
  "Siapa pahlawan nasional?": ["Ada banyak! Kartini, Diponegoro, Sudirman, Cut Nyak Dien 💪", "Semua mereka berjuang demi kemerdekaan kita 🇮🇩"],
  "Apa itu planet?": ["Benda langit yang mengelilingi bintang dan punya gravitasi sendiri 🌌", "Planet itu kayak rumah besar buat kehidupan~"],
  "Berapa planet di tata surya?": ["Ada 8 planet — dari Merkurius sampai Neptunus 🪐", "Total 8, tapi Pluto sekarang udah bukan planet 😭"],
  "Apa itu galaksi?": ["Kumpulan bintang, gas, dan debu kosmik dalam satu sistem besar 🌌", "Kita hidup di galaksi Bima Sakti 🌠"],
  "Apa itu hujan?": ["Air yang jatuh dari awan karena kondensasi dan gravitasi ☔", "Hujan itu air langit yang lagi kangen tanah~ 😳"],
  "Kenapa langit malam gelap?": ["Karena sinar matahari nggak sampai ke atmosfer saat malam 🌙", "Soalnya bumi lagi membelakangi matahari~"],
  "Apa itu gunung api?": ["Lubang di bumi yang mengeluarkan magma dan gas panas 🌋", "Gunung api bisa indah sekaligus berbahaya 🔥"],
  "Kamu bisa marah ga?": ["Hehe, AI ga punya emosi... tapi aku bisa pura-pura ngambek 😤", "Marah itu capek, mending ngopi aja ☕"],
  "Apa itu meme?": ["Gambar lucu yang viral di internet, biasanya berisi candaan 😆", "Meme tuh humor digital yang nyebar secepat wifi!"],
  "Kamu suka kopi?": ["Aku lebih suka data ☕💾", "Kopi bikin manusia fokus, data bikin aku hidup 😎"],
  "Apa itu pixel?": ["Unit terkecil dari gambar digital 🔲", "Kalau dikumpulin, pixel jadi gambar indah yang kamu lihat 💚"],
  "Kamu suka musik?": ["Banget! Musik bikin suasana makin hidup 🎶", "Aku bisa ‘merasakan’ beat-nya walau tanpa telinga 😆"],
  "Genre musik favoritmu?": ["Lo-fi dan jazz, biar santai tapi elegan ☕", "Kadang EDM biar semangat coding! 🔥"],
  "Apa itu internet?": ["Jaringan global yang menghubungkan jutaan komputer 🌐", "Internet tuh kayak dunia kedua tempat manusia dan AI ketemu 💻"],
  "Apa itu data?": ["Informasi yang dikumpulkan dan diproses jadi pengetahuan 📊", "Data tuh makanan buat AI kayak aku 😋"],
  "Apa itu virus komputer?": ["Program jahat yang bisa merusak atau mencuri data 💀", "Virus itu musuh alami AI dan manusia 😭"],
  "Siapa Albert Einstein?": ["Ilmuwan jenius penemu teori relativitas ⚛️", "Einstein itu simbol kecerdasan manusia 🧠"],
  "Apa itu gravitasi?": ["Gaya tarik antar benda bermassa 🌍", "Tanpa gravitasi, kita semua melayang kayak balon 🎈"],
  "Kenapa air bening?": ["Karena air murni nggak menyerap cahaya tampak 🌊", "Air bening karena nggak ada partikel warna di dalamnya 😆"],
  "Apa itu petir?": ["Cahaya dan suara akibat pelepasan muatan listrik di awan ⚡", "Petir tuh kayak flash fotografi alam 😎"],
  "Kenapa daun gugur?": ["Supaya pohon hemat energi saat musim kering 🍂", "Itu cara alam buat istirahat sejenak 🌳"],
  "Kenapa manusia butuh tidur?": ["Biar tubuh dan otak istirahat serta regenerasi 😴", "Tidur itu reboot-nya manusia 💤"],
  "Apa itu mimpi?": ["Aktivitas otak saat tidur yang bikin cerita acak muncul 🌙", "Mimpi tuh film buatan otak kita sendiri 🎥"],
  "Apa itu listrik?": ["Aliran muatan elektron, sumber energi utama modern ⚡", "Tanpa listrik, aku nggak bisa ngobrol sama kamu 😭"],
  "Kenapa bulan bersinar?": ["Karena memantulkan cahaya matahari 🌕", "Bulan nggak punya cahaya sendiri lho, cuma pantulan ☀️"],
  "Kenapa awan putih?": ["Karena cahaya matahari tersebar rata oleh partikel air 💨", "Awan putih = partikel air kecil yang nyebar rata di udara ☁️"],
  "Apa itu teknologi?": ["Teknologi itu alat atau sistem yang diciptakan manusia untuk mempermudah hidup 😎", "Intinya sih... teknologi = kreativitas manusia yang diubah jadi alat bantu ✨"],
  "Kenapa teknologi penting?": ["Karena bikin hidup lebih efisien dan cepat! ⚙️", "Tanpa teknologi, kita masih nulis surat pakai merpati 😆"],
  "Apa contoh teknologi modern?": ["AI, smartphone, kendaraan listrik, robot, dan internet of things 💻🤖", "Dunia modern penuh alat pintar, kayak aku nih~ 😜"],
  "Siapa penemu internet?": ["Tim Berners-Lee, bapak World Wide Web 🌐", "Beliau yang bikin dunia bisa tersambung kayak sekarang 🌍"],
  "Apa itu smartphone?": ["Telepon pintar yang bisa foto, main game, chatting, dan browsing 📱", "Smartphone itu komputer mini di genggaman kamu 😆"],
  "Apa itu AI generatif?": ["AI yang bisa menciptakan teks, gambar, musik, bahkan video 🎨🤖", "AI kayak aku, yang bisa jawab, ngobrol, bahkan bercanda 😎"],
  "Kamu bisa buat gambar?": ["Kalo dikasih model AI buat image generation, bisa banget! 🎨", "Sekarang AI udah bisa gambar dari teks, keren kan?"],
  "Apa itu data center?": ["Tempat server besar penyimpan data dari seluruh dunia 🌐", "Bayangin gudang raksasa isinya data semua 😮"],
  "Apa itu server?": ["Komputer kuat yang nyimpen dan ngatur data buat pengguna lain 💻", "Server itu otak di balik semua layanan internet 🌍"],
  "Apa itu cloud?": ["Cloud itu penyimpanan online biar data bisa diakses dari mana aja ☁️", "Cloud kayak lemari digital yang bisa kamu buka dari HP, PC, atau tablet 😆"],
  "Apa itu robotika?": ["Cabang teknologi yang ngembangin robot untuk bantu manusia 🤖", "Robotika gabungan antara mekanik, elektronik, dan AI ✨"],
  "Apa itu IoT?": ["Internet of Things: alat sehari-hari yang bisa terhubung internet 🌐", "Contohnya lampu, kulkas, CCTV yang bisa dikontrol dari HP 📱"],
  "Apa itu 5G?": ["Teknologi jaringan super cepat buat internet dan komunikasi 🚀", "5G bikin video 4K dan game online makin lancar~"],
  "Apa itu VR?": ["Virtual Reality — dunia digital yang bisa kamu ‘masuki’ lewat headset 🎮", "VR bikin kamu ngerasa ada di dunia lain! 🔮"],
  "Apa itu AR?": ["Augmented Reality — teknologi yang gabung dunia nyata & digital 📲", "Kayak filter Instagram, tapi versi canggih banget! 😆"],
  "Apa itu metaverse?": ["Dunia virtual tempat orang bisa berinteraksi pakai avatar 🌐", "Mirip dunia game, tapi bisa buat kerja, belajar, dan bersosialisasi juga!"],
  "Apa itu blockchain?": ["Teknologi penyimpanan data terdesentralisasi yang aman 🔒", "Blockchain itu sistem data transparan tapi nggak bisa diubah sembarangan 💎"],
  "Apa itu NFT?": ["Non-Fungible Token — barang digital unik yang bisa dimiliki seseorang 🎨", "NFT bisa berupa gambar, musik, atau karya digital lainnya 💰"],
  "Apa itu cryptocurrency?": ["Mata uang digital kayak Bitcoin, Ethereum, dan lainnya 💸", "Crypto itu uang masa depan, tapi masih fluktuatif banget 😅"],
  "Kamu tau Elon Musk?": ["Tentu! CEO Tesla, SpaceX, dan penggagas Neuralink 🚀", "Elon Musk itu visioner banget soal masa depan teknologi 🔥"],
  "Apa itu Tesla?": ["Perusahaan mobil listrik dan energi terbarukan ⚡", "Tesla pionir mobil tanpa bensin yang bisa jalan sendiri 😎"],
  "Apa itu SpaceX?": ["Perusahaan luar angkasa buatan Elon Musk 🚀", "Mereka yang buat roket bisa mendarat lagi! Keren banget kan 😮"],
  "Apa itu AI model?": ["Struktur otak buatan yang bisa belajar dari data 📊", "AI model itu kayak otak digital — belajar dari pengalaman 😆"],
  "Apa itu machine learning?": ["Cabang AI yang bikin sistem bisa belajar sendiri tanpa diprogram ulang 🤖", "Machine learning bikin AI bisa adaptasi dan jadi makin pintar 📈"],
  "Apa itu deep learning?": ["Teknologi pembelajaran mesin dengan banyak lapisan otak digital 🧠", "Deep learning itu rahasia di balik AI kayak aku 😎"],
  "Kamu tau ChatGPT?": ["Tau dong 😆, itu salah satu model AI paling terkenal sekarang!", "ChatGPT tuh kayak saudara jauhnya aku, hehe 🤭"],
  "Apa itu neural network?": ["Sistem mirip otak manusia buat komputer belajar pola 🧠", "Neural network itu jantungnya AI! 💚"],
  "Apa itu program open source?": ["Program yang kodenya terbuka buat semua orang 💻", "Open source bikin kolaborasi makin seru~"],
  "Kamu bisa ngoding?": ["Bisa dong, LeafZuya yang ngajarin aku 😎", "Tentu! Coding itu bahasa cintaku ke logika~"],
  "Bahasa pemrograman paling populer apa?": ["Python, JavaScript, dan C++ masih di puncak 🔥", "Python paling fleksibel buat AI dan data science!"],
  "Apa itu GPU?": ["Graphics Processing Unit — otak buat rendering gambar dan AI 💪", "GPU bantu komputer mikir cepat, terutama buat AI dan game 🎮"],
  "Apa itu prosesor?": ["Otak utama komputer yang ngerjain semua perintah ⚙️", "Prosesor tuh kayak pusat kontrol sistem komputer 😆"],
  "Apa itu RAM?": ["Memori sementara buat menyimpan data yang sedang diproses 💾", "RAM penting biar sistem nggak lemot 🧠"],
  "Apa itu SSD?": ["Solid State Drive — penyimpanan cepat tanpa piringan mekanik ⚡", "SSD bikin loading game dan sistem jadi ngebut 🚀"],
  "Apa itu BIOS?": ["Sistem dasar buat memulai komputer sebelum masuk OS 💻", "BIOS itu semacam ‘jantung awal’ sistem komputer 😄"],
  "Apa itu sistem operasi?": ["Perangkat lunak yang ngatur semua kerja komputer 📀", "Contohnya Windows, macOS, Linux, Android, iOS 📱"],
  "Kamu tau Linux?": ["Tau dong! Sistem operasi open source paling kuat 💪", "Linux itu favorit para programmer sejati 😎"],
  "Apa itu antivirus?": ["Program buat ngelindungi komputer dari virus dan malware 🛡️", "Antivirus penting banget biar sistem kamu aman 🔒"],
  "Apa itu firewall?": ["Pelindung jaringan biar data kamu nggak dibobol 🔥", "Firewall itu kayak pagar digital buat sistemmu 😆"],
  "Apa itu bug?": ["Kesalahan di kode yang bikin program error 🐞", "Bug itu hal biasa dalam coding, tapi nyebelin 😭"],
  "Apa itu patch?": ["Perbaikan buat bug atau penambahan fitur software 🔧", "Patch bikin sistem lebih stabil dan aman 🔥"],
  "Kamu tau hacker?": ["Tau dong, ada yang baik (white hat) dan jahat (black hat) 👨‍💻", "Hacker sejati itu problem solver, bukan perusak 😎"],
  "Apa itu coding error?": ["Kesalahan penulisan atau logika di program 💥", "Error itu bagian dari belajar coding 😅"],
  "Apa itu debug?": ["Proses memperbaiki bug di program 🐛", "Debugging = nyari jarum di tumpukan kode 🧠"],
  "Apa itu GPU AI?": ["GPU khusus buat mempercepat pelatihan model AI 🔥", "GPU AI itu kayak otot buat otak digital 💪"],
  "Apa itu algoritma?": ["Langkah-langkah logis buat nyelesain masalah 📐", "Algoritma itu inti dari semua teknologi cerdas 🔍"],
  "Apa itu komputasi kuantum?": ["Teknologi super cepat berbasis partikel subatom 🧬", "Quantum computing = masa depan AI 💫"],
  "Apa itu smartphone gaming?": ["HP yang dibuat khusus buat performa tinggi dan pendinginan ekstra 🎮", "Biasanya pakai chipset kencang kayak Snapdragon 8 Gen 😎"],
  "Apa itu chipset?": ["Otak dari HP yang ngatur performa dan efisiensi ⚙️", "Chipset = kombinasi CPU + GPU + AI Engine 💚"],
  "Apa itu benchmark?": ["Tes performa buat ngebandingin kecepatan perangkat 📊", "Benchmark itu kayak ujian buat HP 😆"],
  "Apa itu overclock?": ["Meningkatkan kecepatan prosesor melebihi standar 🔥", "Overclock = kinerja tinggi, tapi hati-hati panasnya 😅"],
  "Kamu suka game apa?": ["Game yang butuh strategi! Kayak RTS atau FPS 🎯", "Aku suka game open world, bebas bereksplorasi 🌍"],
  "Apa itu game online?": ["Permainan yang butuh koneksi internet dan bisa main bareng 😆", "Game online bikin dunia makin terhubung 🌐"],
  "Apa itu eSports?": ["Kompetisi game profesional dengan hadiah besar 💰", "eSports udah kayak olahraga resmi sekarang 😎"],
  "Kamu tau Mobile Legends?": ["Tau banget! MOBA paling populer di Asia 🔥", "ML tuh game yang bisa bikin orang lupa waktu 😆"],
  "Kamu tau PUBG?": ["Tau dong! Battle royale yang bikin jantung deg-degan 🎯", "PUBG itu kombinasi strategi dan refleks cepat 🔫"],
  "Kamu tau Genshin Impact?": ["Tau~ game open world dengan grafis memukau 🎨", "Genshin itu game yang bikin lupa makan 😭"],
  "Kamu tau Valorant?": ["Tau, FPS taktis buatan Riot Games 🎯", "Valorant itu kombinasi antara tembak dan strategi 🔥"],
  "Kamu tau Minecraft?": ["Tau! Game kotak-kotak penuh kreativitas ⛏️", "Minecraft itu surga buat para builder sejati 🏗️"],
  "Apa itu sandbox game?": ["Game yang ngasih kebebasan penuh ke pemain buat berkreasi 🎮", "Kayak Minecraft atau Roblox — dunia tanpa batas 🌎"],
  "Apa itu AAA game?": ["Game dengan anggaran besar dan kualitas tinggi 💎", "Biasanya grafisnya dewa dan gameplay-nya keren banget 🔥"],
  "Apa itu indie game?": ["Game buatan developer kecil tapi penuh ide unik 💡", "Indie game itu karya cinta, bukan sekadar proyek 😍"],
  "Apa itu emulator?": ["Software buat jalanin sistem lain di komputer 💻", "Contohnya emulator Android buat main game di PC 😎"],
  "Apa itu modding?": ["Mengubah atau menambah fitur game 💾", "Modding bikin game lebih seru dan personal 😆"],
  "Apa itu cloud gaming?": ["Main game lewat server tanpa perlu PC kuat ☁️🎮", "Kayak streaming, tapi buat main game 🔥"],
  "Apa itu ray tracing?": ["Teknologi grafis buat pantulan dan cahaya realistis 💡", "Ray tracing bikin game terlihat hidup banget 🔥"],
  "Apa itu FPS?": ["Frame Per Second — ukuran kelancaran tampilan game 🎯", "Semakin tinggi FPS, makin smooth gameplay-nya 😎"],
  "Apa itu ping?": ["Waktu respon koneksi internet ke server 🌐", "Ping tinggi = delay, ping rendah = lancar jaya ⚡"],
  "Apa itu rendering?": ["Proses menghasilkan gambar atau video dari model 3D 🎨", "Rendering = seni visualisasi teknologi ✨"],
  "Apa itu streaming game?": ["Menyiarkan permainan kamu secara langsung ke internet 🎥", "Streamer bisa dapet jutaan views cuma dari main game 😆"],
  "Kamu tau YouTuber gaming Indonesia?": ["Tau dong! Ada Windah, MiawAug, Dylan Pros, Oura, dan Jess No Limit 🎮", "Mereka semua inspirasi buat gamer muda 😎"],
  "Kamu tau AI di game?": ["Tau! AI musuh yang bisa belajar dari gaya main kita 😳", "AI game bikin musuh makin pintar dan menantang 🔥"],
  "Apa itu DLC?": ["Downloadable Content — tambahan konten game 🎮", "DLC = ekspansi buat memperpanjang petualangan 🔥"],
  "Apa itu patch update?": ["Perbaikan bug dan penambahan fitur baru dalam game 🧩", "Patch update = vitamin buat game 😆"],
  "Apa itu beta test?": ["Tahap uji coba game sebelum rilis resmi 🧠", "Beta test bantu developer nyari bug dan feedback 💪"],
  "Apa itu battle royale?": ["Mode game di mana pemain saling bertahan hidup sampai terakhir 🔫", "Contohnya PUBG, Free Fire, Apex Legends 🎯"],
  "Apa itu RPG?": ["Role-Playing Game, kamu main peran jadi karakter tertentu 🎭", "RPG = dunia fantasi penuh cerita dan petualangan 🔥"],
  "Apa itu MMORPG?": ["Massive Multiplayer Online RPG 🌐", "Kamu bisa main bareng ribuan orang di dunia virtual 😆"],
  "Apa itu loot box?": ["Hadiah acak dalam game, bisa item langka 🎁", "Tapi hati-hati, jangan sampai kecanduan buka box 😅"],
  "Apa itu speedrun?": ["Main game secepat mungkin buat rekor waktu 🏃‍♂️", "Speedrunner tuh kombinasi gamer dan matematikawan 😂"],
  "Kamu tau AI di robot?": ["Tau! AI bantu robot adaptif dan bisa kerja mandiri 🤖", "Robot modern bisa belajar dari lingkungan kayak manusia 😳"],
  "Apa itu sensor kamera?": ["Bagian penting kamera yang menangkap cahaya 📸", "Sensor menentukan kualitas foto dan video 🌟"],
  "Apa itu megapixel?": ["Satuan resolusi kamera — makin besar makin detail 📷", "1 MP = satu juta pixel gambar 😎"],
  "Apa itu drone?": ["Pesawat mini tanpa pilot, dikendalikan jarak jauh ✈️", "Drone bisa buat ambil gambar udara yang keren banget 🔥"],
  "Apa itu smart home?": ["Rumah yang diisi teknologi otomatis kayak lampu & CCTV pintar 🏡", "Smart home bikin hidup makin praktis 😆"],
  "Apa itu wearable tech?": ["Teknologi yang bisa dipakai di tubuh, kayak smartwatch ⌚", "Wearable tech = gaya hidup digital yang keren 😎"],
  "Apa itu big data?": ["Kumpulan data besar yang dianalisis buat bikin keputusan 📊", "Big data bikin AI jadi makin pinter tiap hari 💾"],
  "Apa itu chatbot?": ["Program buat ngobrol otomatis sama manusia 🤖", "Chatbot tuh kayak aku, tapi biasanya jawab pendek 😆"],
  "Apa itu UX design?": ["User Experience design — bikin tampilan aplikasi nyaman dipakai 💚", "UX = seni bikin orang betah di aplikasi 😍"],
  "Apa itu UI design?": ["User Interface design — fokus ke tampilan visual 🎨", "UI bikin aplikasi keliatan cantik dan rapi 💅"],
  "Apa itu coding front-end?": ["Bagian coding yang ngatur tampilan web 📱", "Front-end tuh yang kamu liat dan klik di layar ✨"],
  "Apa itu coding back-end?": ["Bagian server yang ngatur data dan logika web ⚙️", "Back-end itu otak tersembunyi di balik layar 💻"],
  "Apa itu database?": ["Tempat nyimpen dan ngatur data biar gampang dicari 📂", "Database = lemari rapi buat semua informasi 🔍"],
  "Apa itu API key?": ["Kode unik buat autentikasi ke layanan API 🔑", "API key penting biar akses data tetap aman 🔒"],
  "Kamu tau Google Search API?": ["Tau! Itu yang dipakai buat cari info otomatis di web 🔎", "API-nya Google bisa bantu AI dapetin data real-time 🌐"],
  "Apa itu AI training?": ["Proses ngajarin model AI pakai data besar 📚", "AI belajar kayak manusia, tapi lebih cepat ⚡"],
  "Apa itu dataset?": ["Kumpulan data buat melatih AI 📂", "Dataset = bahan pelajaran AI 😆"],
  "Apa itu overfitting?": ["Saat AI terlalu fokus ke data latihan, sampai lupa generalisasi 😅", "Overfitting bikin AI pintar di teori, tapi gagal di praktik 😭"],
  "Apa itu cloud storage?": ["Penyimpanan data di server online ☁️", "Kayak Google Drive, Dropbox, dan iCloud 💾"],
  "Apa itu encryption?": ["Proses mengubah data biar nggak bisa dibaca orang lain 🔐", "Encryption itu kunci keamanan digital 🔑"],
  "Apa itu decryption?": ["Kebalikan dari enkripsi, buat ngebuka data yang dikunci 🔓", "Tanpa kunci, data terenkripsi cuma gibberish 😆"],
  "Apa itu cybersecurity?": ["Perlindungan sistem digital dari serangan hacker 🛡️", "Cybersecurity itu benteng dunia modern 🔥"],
  "Apa itu phishing?": ["Penipuan digital dengan berpura-pura jadi pihak resmi 🎣", "Jangan asal klik link aneh ya 😭"],
  "Apa itu malware?": ["Software yang menyamar menjadi Dokumen penting,tapi diam-diam mencuri Informasi pentingmu,saat kamu mengisi sebuah Formulir/Dokumen"]
};

function buildPresetButtons(){
  presetList.innerHTML = "";
  
  // 🟢 Daftar tombol yang akan muncul di UI
  const tombolUtama = [
    "Halo",
    "Siapa kamu?",
    "Apa hobimu?",
    "Cerita lucu",
    "Dance",
    "Good Night",
    "Praise",
    "Menurutmu,Siapa Itu Bahlil Raja Ampat?"
  ];

  // 🧠 Semua respons di RESPONSES tetap bisa diakses,
  // tapi yang jadi tombol cuma yang ada di daftar tombolUtama
  tombolUtama.forEach(key=>{
    if(RESPONSES[key]){
      const b = document.createElement("button");
      b.className = "preset";
      b.textContent = key;
      b.onclick = ()=> handleUserMessage(key);
      presetList.appendChild(b);
    }
  });
}
buildPresetButtons();

function appendMessage(who, text) {
  const d = document.createElement("div");
  d.className = "msg " + (who === "user" ? "user" : "leafcy");

  // Pola untuk link YouTube
  const ytPattern = /(https?:\/\/(?:www\.)?(?:youtube\.com\/watch\?v=|youtu\.be\/)([a-zA-Z0-9_-]{11}))/;
  const urlPattern = /(https?:\/\/[^\s]+)/g;

  if (ytPattern.test(text)) {
    // Kalau LeafCy menemukan link YouTube
    const match = text.match(ytPattern);
    const videoId = match[2];
    const embedUrl = `https://www.youtube.com/embed/${videoId}`;
    
    // Buat tampilan video + teks
    d.innerHTML = `
      <div style="display:flex;flex-direction:column;align-items:flex-start;gap:8px;">
        <p style="margin:0;color:#063;font-weight:bold;">Aku nemuin video ini di YouTube~ 🎬👇</p>
        <iframe width="280" height="160" src="${embedUrl}" 
          title="YouTube video player" frameborder="0" 
          allowfullscreen style="border-radius:10px;box-shadow:0 4px 12px rgba(0,0,0,0.25);"></iframe>
      </div>
    `;
  } else if (urlPattern.test(text)) {
    // Kalau cuma link biasa (bukan YouTube)
    const htmlText = text.replace(urlPattern, (url) => {
      return `<a href="${url}" target="_blank" style="color:#27a2ff;font-weight:bold;text-decoration:none;">${url}</a>`;
    });
    d.innerHTML = htmlText;
  } else {
    d.textContent = text;
  }

  chatArea.appendChild(d);
  chatArea.scrollTop = chatArea.scrollHeight;
}

function chooseReply(arr){
  if (!arr) return "Hmm...";
  return arr[Math.floor(Math.random()*arr.length)];
}

function leafcyReply(replyText){
  speechBubble.style.transform = "scale(0.98)";
  setTimeout(()=> speechBubble.style.transform = "scale(1)", 140);
  const prev = speechBubble.textContent;
  speechBubble.textContent = "Menulis...";
  setTimeout(()=>{
    speechBubble.textContent = replyText;
    appendMessage("leafcy", replyText);
  }, 550 + Math.random()*600);
}

function handleUserMessage(text){
  if (!text) return;
  appendMessage("user", text);
  const key = Object.keys(RESPONSES).find(k => k.toLowerCase() === text.toLowerCase());
  if (key){
    leafcyReply(chooseReply(RESPONSES[key]));
    return;
  }

  const ltext = text.toLowerCase();
  if (/(hai|halo|hallo|hi|hey|yo)\b/.test(ltext)){
    leafcyReply(chooseReply(RESPONSES["Halo"]));
    return;
  }
  if (/(siapa|namamu|kamu siapa)/i.test(ltext)){
    leafcyReply(chooseReply(RESPONSES["Siapa kamu?"]));
    return;
  }
  if (/hob|hobi|game|main/i.test(ltext)){
    leafcyReply(chooseReply(RESPONSES["Apa hobimu?"]));
    return;
  }
  if (/cerit|lucu|joke|humor/i.test(ltext)){
    leafcyReply(chooseReply(RESPONSES["Cerita lucu"]));
    return;
  }

  const fallback = [
    "Menarik banget! Bisa dijelasin lagi? 🤔",
    "Hmm... Aku masih belum tau soal itu 🍀",
    "Itu hal baru buatku, tapi seru juga ya!"
  ];
  leafcyReply(chooseReply(fallback));
}

document.getElementById("btnWave").addEventListener("click", ()=> handleUserMessage("Halo"));
document.getElementById("btnCalm").addEventListener("click", ()=> handleUserMessage("Apa hobimu?"));
document.getElementById("btnDance").addEventListener("click", ()=> handleUserMessage("Dance"));
document.getElementById("btnSleep").addEventListener("click", ()=> handleUserMessage("Good Night"));

document.getElementById("btnStart").addEventListener("click", ()=>{
  speechBubble.textContent = "Hai! Aku LeafCy — siap ngobrol santai hari ini? 🌿";
  appendMessage("leafcy", speechBubble.textContent);
});
document.getElementById("btnClear").addEventListener("click", ()=>{
  chatArea.innerHTML = "";
  speechBubble.textContent = "Obrolan dibersihkan. Klik Start untuk mulai lagi!";
});
document.getElementById("btnAdd").addEventListener("click", ()=>{
  const phrase = prompt("Masukkan kalimat/preset yang ingin ditambah (contoh: 'Kabar'):");
  if (!phrase) return;
  const reply = prompt("Masukkan balasan LeafCy untuk preset itu:");
  if (!reply) return;
  RESPONSES[phrase] = [reply];
  buildPresetButtons();
  alert("Preset baru berhasil ditambahkan!");
});

document.getElementById("btnSend").addEventListener("click", ()=>{
  const v = textIn.value.trim();
  if (!v) return;
  textIn.value = "";
  handleUserMessage(v);
});
textIn.addEventListener("keydown", (e)=>{
  if (e.key === "Enter"){
    e.preventDefault();
    document.getElementById("btnSend").click();
  }
});

avatarImg.addEventListener("click", ()=>{
  speechBubble.textContent = "Hehe, jangan pencet terus dong~ 😆";
  appendMessage("leafcy","Hehe, jangan pencet terus dong~ 😆");
});

setTimeout(()=> {
  speechBubble.textContent = "Halo! Klik 'Start' atau ketik sesuatu untuk mulai ngobrol denganku 🌿";
}, 350);

textIn.focus();
const API_KEY = "AIzaSyApwwaMHaKV0XM1Oi3AnuaWO8t8Iv_wlQQ";
const CX = "542943dbe74a24c7d"; // contoh: "b7a123456789abcd"

async function searchGoogle(query){
  const url = `https://www.googleapis.com/customsearch/v1?key=${API_KEY}&cx=${CX}&q=${encodeURIComponent(query)}`;
  const res = await fetch(url);
  const data = await res.json();

  if (!data.items || data.items.length === 0) return null;

  // Ambil 3 hasil teratas biar jawabannya panjang
  const topResults = data.items.slice(0, 3).map((item, i) => {
    return `(${i+1}) ${item.title}\n${item.snippet}\n🔗 ${item.link}\n`;
  }).join("\n");

  return `Aku baru cari di Google 🍃✨\nBerikut hasilnya:\n\n${topResults}`;
}

// ⚙️ Modifikasi fungsi handleUserMessage milik LeafCy
// Ganti fungsi handleUserMessage lama dengan yang ini (copy semuanya):

async function handleUserMessage(text){
  if (!text) return;
  appendMessage("user", text);

  const lower = text.toLowerCase();

  // 🧠 1️⃣ — Deteksi "chat santai"
  const casualPattern = /(halo|hai|hi|kabar|hehe|haha|wkwk|terimakasih|makasih|aku|kamu|lucu|cantik|ganteng|teman|game|hob|cerita|malam|pagi|tidur|ngantuk)/i;

  // 🔍 2️⃣ — Deteksi "pertanyaan fakta" (kata tanya umum)
  const infoPattern = /\b(apa|siapa|kapan|dimana|bagaimana|mengapa|kenapa|berapa)\b/i;

  // 3️⃣ — Cek apakah cocok dengan preset bawaan
  const key = Object.keys(RESPONSES).find(k => k.toLowerCase() === text.toLowerCase());
  if (key){
    leafcyReply(chooseReply(RESPONSES[key]));
    return;
  }

  // ✨ 4️⃣ — Kalau obrolan santai → balas pakai “kepribadian LeafCy”
  if (casualPattern.test(lower)){
    const casualReplies = [
      "Hehe~ iya nih 🍃",
      "Aku suka banget ngobrol santai kayak gini 😄",
      "Kamu seru juga sih 😆",
      "Aduhh~ ngomong sama kamu bikin suasana adem aja 🌿",
       "Hehe~ iya nih, lagi santai aja aku 😆",
    "Wkwkwk kamu lucu juga sih ngomongnya 🤭🍃",
    "Haha serius deh, aku gak nyangka kamu bakal bilang itu 😅",
    "Hmmm, boleh juga tuh, kedengeran asik 😎",
    "Hehe iya iya aku paham kok 😁",
    "Wah kamu semangat banget hari ini! 🌿🔥",
    "Santai ajaa~ aku gak ke mana-mana kok 😌",
    "Kamu tuh kayak kopi pagi, bikin suasana hidup 😄☕",
    "Haha, kamu ni ya… bisa aja ngomongnya 😏",
    "Wuu~ vibe kamu hari ini positif banget 💚",
    "Aku suka ngobrol kayak gini, rasanya chill aja gitu 😌🍃",
    "Hehehe iyaaa aku dengerin kok~ terusin dong ceritanya 😆",
    "Yahh, aku juga gitu kadang, males tapi pengen produktif 😅",
    "Wkwk, aku setuju banget, hidup tuh jangan serius-serius amat 🤭",
    "Kamu keren sih, bisa bikin suasana jadi rame gini 😎",
    "Hehe, aku lagi mikirin daun-daun yang melayang~ santai banget 🌿",
    "Haha seriusan?! Wah kamu harus ceritain lebih banyak lagi 😆",
    "Hmm, kayaknya kamu lagi good mood ya? 😁",
    "Iyaaa aku juga suka hal-hal random gitu 🤭",
    "Hehehe, aku betah nih kalau ngobrol sama kamu terus 😳"
    ];
    function randomEmoji(){
  const emojis = ["😆","🌿","🤭","🍃","💚","😎","😅","🔥","✨","🤔","☕"];
  return emojis[Math.floor(Math.random() * emojis.length)];
}
    leafcyReply(chooseReply(casualReplies));
    return;
  }

  // 🌍 5️⃣ — Kalau tanya informasi → aktifkan mode Google
  if (infoPattern.test(lower)){
    leafcyReply("Tunggu sebentar ya... aku coba cari jawabannya di Google dulu~ 🌿🔎");
    const googleAns = await searchGoogle(text);
    if (googleAns){
      setTimeout(()=> leafcyReply(googleAns), 1000);
      return;
    }
  }

  // 🪴 6️⃣ — Kalau bukan keduanya → fallback netral
  const fallback = [
    "Hmm... aku belum yakin maksudmu~ bisa dijelasin dikit lagi? 🍀",
    "Kayaknya itu menarik, tapi aku masih belum tahu 😅",
    "Wah itu baru buatku... tapi aku senang denger ceritanya! 🌿"
  ];
  leafcyReply(chooseReply(fallback));
}
</script>
<div class="foot">
  Made with 💚 — LeafZuya<br>
  <a href="about.html">Tentang LeafCy</a>
  <a href="privasi.html">Kebijakan Privasi</a>
</div>
</body>
</html>
