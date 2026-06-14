<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport"
content="width=device-width, initial-scale=1.0, viewport-fit=cover">
<title>(주)청송 임직원 인증 시스템</title>

<link href="https://fonts.googleapis.com/css2?family=Song+Myung&display=swap" rel="stylesheet">

<style>
*{
    margin:0;
    padding:0;
    box-sizing:border-box;
}

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
    position:absolute;
    white-space:nowrap;
    line-height:50px;
    font-size:1.3rem;
    letter-spacing:2px;
    color:#d0d0d0;
    text-shadow:
        0 0 10px #fff,
        0 0 20px #999,
        0 0 30px #555;
    animation:bannerScroll 6s linear infinite;
}

@keyframes bannerScroll{
    from{
        transform:translateX(100%);
    }
    to{
        transform:translateX(-100%);
    }
}

body{
    min-height:100vh;
    min-height:100dvh;
    display:flex;
    justify-content:center;
    align-items:center;
    padding:20px;
    padding-top:50px;
    background:#000;
    color:#d8d8d8;
    font-family:'Song Myung', serif;
}

/* 노이즈 효과 */
body::before{
    content:"";
    position:fixed;
    top:0;
    left:0;
    width:100%;
    height:100%;
    background:
    repeating-radial-gradient(
        rgba(255,255,255,0.02) 0px,
        rgba(255,255,255,0.02) 1px,
        transparent 2px,
        transparent 4px
    );
    opacity:.15;
    pointer-events:none;
}

.container{
    width:90%;
    max-width:360px;
    padding:20px;
    text-align:center;
    animation:fadeIn 1.5s;
}
    
.loading-screen{
    text-align:center;
}

.loading-bar{
    width:300px;
    height:20px;
    border:1px solid #555;
    margin:20px auto;
}

.progress{
    width:0%;
    height:100%;
    background:#777;
}

.main-header{
    padding:20px;
    border-bottom:1px solid #222;
    text-align:center;
}

.main-header nav a{
    color:#ccc;
    text-decoration:none;
    margin:0 10px;
}

.hero{
    padding:60px 20px;
    text-align:center;
}

.cards{
    display:flex;
    flex-wrap:wrap;
    justify-content:center;
    gap:20px;
    padding:20px;
}

.card{
    width:250px;
    border:1px solid #222;
    padding:20px;
    background:#050505;
}

footer{
    text-align:center;
    padding:30px;
    color:#555;
}
    
.logo{
    letter-spacing:10px;
    text-shadow:
    0 0 5px rgba(255,255,255,.3),
    0 0 20px rgba(255,255,255,.1);
}

.message{
    font-size:1.4rem;
    line-height:1.6;
    margin-bottom:25px;
    margin-bottom:30px;
    min-height:80px;
}

input{
    width:100%;
    max-width:320px;
    padding:16px;
    font-size:16px;
    padding:15px;
    background:#050505;
    border:1px solid #444;
    color:#ddd;
    text-align:center;
    font-size:1.2rem;
    outline:none;
    font-family:Arial,sans-serif;
}

input:focus{
    border-color:#888;
    box-shadow:0 0 15px rgba(255,255,255,.15);
}

button{
    width:100%;
    max-width:320px;
    padding:15px;
    margin-top:15px;
    font-size:1rem;
    background:#111;
    color:#ccc;
    border:1px solid #555;
    cursor:pointer;
}

button:hover{
    animation:glitch .15s infinite;
}

.footer{
    margin-top:40px;
    font-size:.8rem;
    color:#555;
    letter-spacing:2px;
}

.red{
    color:#a30000;
    text-shadow:0 0 10px red;
}

@keyframes fadeIn{
    from{
        opacity:0;
        transform:translateY(20px);
    }
    to{
        opacity:1;
        transform:translateY(0);
    }
}

@keyframes glitch{
    0%{transform:translate(1px,-1px);}
    25%{transform:translate(-1px,1px);}
    50%{transform:translate(2px,0);}
    75%{transform:translate(-2px,0);}
    100%{transform:translate(0,0);}
}

.flash{
    animation:flash .2s;
}

@keyframes flash{
    0%{filter:brightness(5);}
    100%{filter:brightness(1);}
}
</style>
</head>
<body>

<div class="top-banner">
    <div class="banner-track">
        ☢ 청송그룹에 오신 것을 환영합니다 =) ☢ 청송그룹에 오신 것을 환영합니다 =) ☢ 청송그룹에 오신 것을 환영합니다 =) ☢ 청송그룹에 오신 것을 환영합니다 =)
    </div>
</div>

<div class="container" id="container">

    <div class="logo">(주)청송</div>

    <div class="message" id="message">
        담당 계열사를 입력해주세요.
    </div>

    <input type="text" id="input">

    <br>

    <button onclick="nextStep()">확인</button>

    <div class="footer" id="footer">
        AUTHORIZED PERSONNEL ONLY
    </div>

</div>

<script>

let step = 1;
let company = "";
let team = "";

const message = document.getElementById("message");
const input = document.getElementById("input");
const footer = document.getElementById("footer");
const container = document.getElementById("container");

input.addEventListener("keypress", function(e){
    if(e.key === "Enter"){
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

    if(value === "") return;

    flash();

    if(step === 1){

        company = value;

        setTimeout(()=>{
            message.innerHTML =
            "계열사 확인 완료.<br><br>담당 팀을 입력해주세요.";
            footer.innerHTML = "기록이 검증되고 있습니다...";
            input.value = "";
            step = 2;
        },300);

    }

    else if(step === 2){

        team = value;

        setTimeout(()=>{
            message.innerHTML =
            "담당 팀 확인 완료.<br><br>담당 코드를 입력해주세요.";
            footer.innerHTML = "AUTHORIZATION REQUIRED";
            input.value = "";
            step = 3;
        },300);

    }

    else if(step === 3){

        if(value === "240314"){

    document.body.innerHTML = `
    <div class="loading-screen">
        <h1>청송 중앙망 접속 중...</h1>

        <div class="loading-bar">
            <div class="progress" id="progress"></div>
        </div>

        <p id="percent">0%</p>
        <p>내부 기록 동기화 중...</p>
    </div>
    `;

    let width = 0;

    const interval = setInterval(() => {

        width++;

        document.getElementById("progress").style.width = width + "%";
        document.getElementById("percent").innerText = width + "%";

        if(width >= 100){

            clearInterval(interval);

            showHomepage();
        }

    },30);
}
            function showHomepage(){

document.body.innerHTML = `

<header class="main-header">

    <div class="company-name">
        (주)청송
    </div>

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
    1997년 설립 이후 청송은
    보존·분석·관찰 기술을 연구하며
    지속 가능한 정보 관리 체계를 구축하고 있습니다.
    </p>

</section>

<section class="cards">

    <div class="card">
        <h2>연구사업</h2>
        <p>관찰 및 분석 시스템 개발</p>
    </div>

    <div class="card">
        <h2>계열사</h2>
        <p>청송정보통신<br>청송물산<br>청송연구원</p>
    </div>

    <div class="card">
        <h2>공지사항</h2>
        <p>제11차 기록보존규약 개정</p>
    </div>

</section>

<footer>
    모든 기록은 보존됩니다.
</footer>

`;
}

                <div class="message">
                    ㈜청송 내부망 접속이 허가되었습니다.
                    <br><br>
                    접속 일시
                    <br>
                    ${new Date().toLocaleString()}
                </div>

                <div class="footer">
                    기록은 보존됩니다.
                </div>
            </div>
            `;

        }else{

            document.body.innerHTML = `
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
</script>

</body>
</html>
