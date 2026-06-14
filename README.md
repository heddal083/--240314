<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
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
    text-align:center;
    width:600px;
    animation:fadeIn 1.5s;
}

.logo{
    letter-spacing:10px;
    text-shadow:
    0 0 5px rgba(255,255,255,.3),
    0 0 20px rgba(255,255,255,.1);
}

.message{
    font-size:2rem;
    margin-bottom:30px;
    min-height:80px;
}

input{
    width:350px;
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
    margin-top:20px;
    padding:12px 40px;
    background:#111;
    color:#ccc;
    border:1px solid #555;
    cursor:pointer;
    font-size:1rem;
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
            <div class="container">
                <div class="logo">인증 완료</div>

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
