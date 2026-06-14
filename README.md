<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport"
content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>(주)청송</title>
<meta name="apple-mobile-web-app-title" content="(주)청송">

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
    font-family:'Song Myung', serif;
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

document.body.innerHTML = `

<style>

body{
    margin:0;
    background:#000;
    color:#d8d8d8;
    font-family:'Song Myung', serif;
    overflow:hidden;
}

body::before{
    content:"";
    position:fixed;
    inset:0;
    background:
    repeating-linear-gradient(
        45deg,
        #050505,
        #050505 10px,
        #080808 10px,
        #080808 20px
    );
    opacity:.35;
    pointer-events:none;
}

.portal{
    display:flex;
    height:100vh;
}

.sidebar{
    width:280px;
    background:#030303;
    border-right:1px solid #222;
    padding:20px;
    overflow-y:auto;
}

.employee{
    border:1px solid #222;
    padding:15px;
    margin-bottom:20px;
    background:#080808;
}

.employee h3{
    margin-top:0;
}

.menu{
    margin-top:20px;
}

.menu-item{
    padding:14px;
    border-bottom:1px solid #151515;
    cursor:pointer;
}

.menu-item:hover{
    background:#111;
}

.content{
    flex:1;
    padding:40px;
    overflow-y:auto;
}

.title{
    font-size:2rem;
    margin-bottom:20px;
}

.card{
    background:#050505;
    border:1px solid #222;
    padding:20px;
    margin-bottom:20px;
}

.card h2{
    margin-top:0;
}

table{
    width:100%;
    border-collapse:collapse;
}

td,th{
    border:1px solid #222;
    padding:10px;
}

.footer-note{
    position:fixed;
    bottom:15px;
    right:20px;
    color:#444;
    font-size:.8rem;
}

</style>

<div class="portal">

<div class="sidebar">

<div class="employee">

<h3>사원 정보</h3>

<p>사번 : CS-240314</p>
<p>부서 : 연구개발본부</p>
<p>직급 : 선임연구원</p>

</div>

<div class="menu">

<div class="menu-item" onclick="showPage('intro')">
회사 소개
</div>

<div class="menu-item" onclick="showPage('research')">
연구산업
</div>

<div class="menu-item" onclick="showPage('drug')">
신약 목록
</div>

<div class="menu-item" onclick="showPage('archive')">
보존 기록
</div>

<div class="menu-item" onclick="showPage('network')">
내부망
</div>

</div>

</div>

<div class="content" id="content">

<h1 class="title">CS화학</h1>

<div class="card">

<h2>회사 소개</h2>

<p>

CS화학은 청송그룹 산하 화학·생명공학 계열사입니다.

<br><br>

당사는 생명공학, 재생의학, 합성화학,
차세대 보존기술 연구를 수행하고 있습니다.

<br><br>

기록은 자산이며,
보존은 미래를 위한 투자입니다.

</p>

</div>

</div>

</div>

<div class="footer-note">

CS CHEMICALS ARCHIVE SYSTEM v3.14

</div>

`;

window.showPage = function(page){

const content = document.getElementById("content");

if(page==="intro"){

content.innerHTML = `

<h1 class="title">CS화학</h1>

<div class="card">

<h2>회사 소개</h2>

<p>

CS화학은 청송그룹 산하 화학 연구 계열사입니다.

<br><br>

바이오, 화학, 의약품 연구를 수행하며
차세대 기술 개발에 집중하고 있습니다.

</p>

</div>

`;

}

else if(page==="research"){

content.innerHTML = `

<h1 class="title">연구산업</h1>

<div class="card">

<ul>

<li>바이오 신약 연구</li>
<li>세포 재생 기술</li>
<li>합성 화합물 개발</li>
<li>생체 보존 기술</li>
<li>차세대 의약소재 연구</li>

</ul>

</div>

`;

}

else if(page==="drug"){

content.innerHTML = `

<h1 class="title">신약 목록</h1>

<div class="card">

<table>

<tr>
<th>코드명</th>
<th>분류</th>
<th>상태</th>
</tr>

<tr>
<td>CS-01</td>
<td>신경 안정제</td>
<td>개발 완료</td>
</tr>

<tr>
<td>CS-12</td>
<td>재생 촉진제</td>
<td>임상 진행</td>
</tr>

<tr>
<td>CS-44</td>
<td>세포 보존제</td>
<td>연구 단계</td>
</tr>

</table>

</div>

`;

}

else if(page==="archive"){

content.innerHTML = `

<h1 class="title">보존 기록</h1>

<div class="card">

기록번호 #2034<br>
보존 완료<br>
2026.04.12

</div>

<div class="card">

기록번호 #2178<br>
보존 완료<br>
2026.05.29

</div>

<div class="card">

기록번호 #2211<br>
열람 제한<br>
등급 : 내부

</div>

`;

}

else if(page==="network"){

content.innerHTML = `

<h1 class="title">내부망</h1>

<div class="card">

공지사항

<br><br>

- 연구동 B구역 점검 예정
<br>
- 연구보고서 제출 안내
<br>
- 보존실 출입 규정 개정

</div>

<div class="card">

최근 접속 기록

<br><br>

2026.06.14
<br>
연구개발본부

</div>

`;

}

}

}
</script>
</body>
</html>
