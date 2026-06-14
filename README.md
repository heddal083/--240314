<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>(주)청송 임직원 인증 시스템</title>
<link href="https://fonts.googleapis.com/css2?family=Song+Myung&display=swap" rel="stylesheet">
<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}
body{
    background:#000;
    color:#d8d8d8;
    min-height:100vh;
    min-height:100dvh;
    display:flex;
    justify-content:center;
    align-items:center;
    padding:70px 20px 20px 20px;
    font-family:'Song Myung', serif;
    overflow-x:hidden;
}
/* 노이즈 효과 */
body::before{
    content:"";
    position:fixed;
    inset:0;
    background:
    repeating-radial-gradient(
        rgba(255,255,255,.02) 0px,
        rgba(255,255,255,.02) 1px,
        transparent 2px,
        transparent 4px
    );
    pointer-events:none;
}
/* 상단 배너 */
.top-banner{
    position:fixed;
    top:0;
    left:0;
    width:100%;
    height:50px;
    background:#050505;
    border-bottom:1px solid #222;
    overflow:hidden;
    z-index:9999;
}
.banner-track{
    white-space:nowrap;
    line-height:50px;
    font-size:1rem;
    color:#d0d0d0;
    animation:bannerScroll 8s linear infinite;
    text-shadow:
        0 0 5px rgba(255,255,255,.4),
        0 0 15px rgba(255,255,255,.1);
}
@keyframes bannerScroll{
    from{
        transform:translateX(100%);
    }
    to{
        transform:translateX(-100%);
    }
}
.container{
    width:90%;
    max-width:360px;
    text-align:center;
}
.logo{
    font-size:2.3rem;
    margin-bottom:30px;
    letter-spacing:6px;
    font-family:'Song Myung', serif;
    text-shadow:
        0 0 5px rgba(255,255,255,.25),
        0 0 20px rgba(255,255,255,.08);
}
.message{
    font-size:1.3rem;
    line-height:1.7;
    margin-bottom:25px;
    min-height:100px;
    font-family:'Song Myung', serif;
}
input{
    width:100%;
    padding:16px;
    background:#050505;
    border:1px solid #333;
    color:#ddd;
    text-align:center;
    font-size:16px;
    outline:none;
    font-family:'Song Myung', serif;
}
input:focus{
    border-color:#777;
    box-shadow:0 0 15px rgba(255,255,255,.1);
}
button{
    width:100%;
    margin-top:15px;
    padding:15px;
    background:#111;
    border:1px solid #444;
    color:#ddd;
    cursor:pointer;
    font-family:'Song Myung', serif;
}
button:hover{
    opacity:.85;
}
.footer{
    margin-top:30px;
    font-size:.8rem;
    color:#666;
}
.flash{
    animation:flash .2s;
}
@keyframes flash{
    0%{filter:brightness(4);}
    100%{filter:brightness(1);}
}
/* 로딩 */
.loading-screen{
    text-align:center;
    width:90%;
    max-width:400px;
}
.loading-screen h1{
    margin-bottom:20px;
}
.loading-bar{
    width:100%;
    height:22px;
    border:1px solid #444;
    margin:20px 0;
}
.progress{
    width:0%;
    height:100%;
    background:#888;
}
.loading-screen p{
    margin-top:10px;
}
/* 홈페이지 */
.homepage{
    width:100%;
    max-width:1200px;
}
.main-header{
    border-bottom:1px solid #222;
    padding:20px;
    text-align:center;
}
.company-name{
    font-size:2rem;
    margin-bottom:15px;
}
.main-header nav{
    display:flex;
    justify-content:center;
    flex-wrap:wrap;
    gap:15px;
}
.main-header nav a{
    color:#ccc;
    text-decoration:none;
}
.hero{
    padding:70px 20px;
    text-align:center;
}
.hero h1{
    margin-bottom:20px;
}
.hero p{
    line-height:1.8;
    color:#aaa;
}
.cards{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:20px;
    padding:20px;
}
.card{
    width:300px;
    background:#050505;
    border:1px solid #222;
    padding:20px;
}
.card h2{
    margin-bottom:15px;
}
.card p{
    line-height:1.8;
    color:#aaa;
}
footer{
    text-align:center;
    padding:40px;
    color:#555;
}
.red{
    color:#8d0000;
}
</style>
</head>
<body>
<div class="top-banner">
    <div class="banner-track">
        ☢ 청송그룹에 오신 것을 환영합니다 =) ☢ 청송그룹에 오신 것을 환영합니다 =) ☢ 청송그룹에 오신 것을 환영합니다 =) ☢
    </div>
</div>
<div class="container" id="container">
<div class="logo">(주)청송</div>
<div class="message" id="message">
    담당 계열사를 입력해주세요.
</div>
<input type="text" id="input">
<button onclick="nextStep()">확인</button>
<div class="footer" id="footer">
    AUTHORIZED PERSONNEL ONLY
</div>
</div>
<script>
let step = 1;
const message = document.getElementById("message");
const input = document.getElementById("input");
const footer = document.getElementById("footer");
const container = document.getElementById("container");
input.addEventListener("keypress",function(e){
    if(e.key==="Enter"){
        nextStep();
    }
});
function flash(){
    container.classList.add("flash");
    setTimeout(()=>{
        container.classList.remove("flash");
    },200);
}
function nextStep(){
    const value = input.value.trim();
    if(value==="") return;
    flash();
    if(step===1){
        setTimeout(()=>{
            message.innerHTML=
            "계열사 확인 완료.<br><br>담당 팀을 입력해주세요.";
            footer.innerHTML="기록 검증 중...";
            input.value="";
            step=2;
        },300);
    }
    else if(step===2){
        setTimeout(()=>{
            message.innerHTML=
            "담당 팀 확인 완료.<br><br>담당 코드를 입력해주세요.";
            footer.innerHTML="AUTHORIZATION REQUIRED";
            input.value="";
            step=3;
        },300);
    }
    else if(step===3){
        if(value==="240314"){
            document.body.innerHTML=`
            <div class="loading-screen">
                <h1>청송 중앙망 접속 중...</h1>
                <div class="loading-bar">
                    <div class="progress" id="progress"></div>
                </div>
                <p id="percent">0%</p>
                <p>내부 기록 동기화 중...</p>
            </div>
            `;
            let width=0;
            const interval=setInterval(()=>{
                width++;
                document.getElementById("progress").style.width=width+"%";
                document.getElementById("percent").innerText=width+"%";
                if(width>=100){
                    clearInterval(interval);
                    showHomepage();
                }
            },25);
        }else{
            document.body.innerHTML=`
            <div class="container">
                <div class="logo red">오류</div>
                <div class="message red">
                인증되지 않은 접근이 감지되었습니다.
                <br><br>
                세션이 기록되었습니다.
                </div>
                <div class="footer">
                SYSTEM LOG CREATED
                </div>
            </div>
            `;
            setTimeout(()=>{
                location.reload();
            },3000);
        }
    }
}
function showHomepage(){
document.body.innerHTML=`
<div class="homepage">
<header class="main-header">
<div class="company-name">(주)청송</div>
<nav>
<a href="#">회사소개</a>
<a href="#">계열사</a>
<a href="#">연구사업</a>
<a href="#">보존기록</a>
<a href="#">내부망</a>
</nav>
</header>
<section class="hero">
<h1>청송은 미래를 기록합니다.</h1>
<p>
청송은 정보 보존, 분석 및 연구를 기반으로
다양한 분야의 데이터 관리 체계를 구축하고 있습니다.
<br><br>
기록은 자산이며,
보존은 곧 미래를 위한 투자입니다.
</p>
</section>
<section class="cards">
<div class="card">
<h2>연구사업</h2>
<p>
정보 분석 연구<br>
기록 보존 기술<br>
관찰 시스템 개발
</p>
</div>
<div class="card">
<h2>계열사</h2>
<p>
청송정보통신<br>
청송물산<br>
청송연구원
</p>
</div>
<div class="card">
<h2>공지사항</h2>
<p>
제11차 기록보존규약 개정<br>
2026.06.14
</p>
</div>
</section>
<footer>
모든 기록은 보존됩니다.
</footer>
</div>
`;
}
</script>
</body>
</html>
