let board = ["","","","","","","","",""];
let human = "X";
let ai = "O";
let gameOver = false;

createBoard();

function createBoard(){
    let boardDiv = document.getElementById("board");
    boardDiv.innerHTML="";

    board.forEach((cell,index)=>{
        let div = document.createElement("div");
        div.classList.add("cell");
        div.innerText = cell;

        div.addEventListener("click",()=>playerMove(index));

        boardDiv.appendChild(div);
    });
}

function playerMove(i){

    if(board[i]!=="" || gameOver) return;

    board[i]=human;
    createBoard();

    if(checkWin(board,human)){
        statusText("Human Wins");
        gameOver=true;
        return;
    }

    aiMove();
}

function aiMove(){

    let bestScore=-Infinity;
    let move;

    for(let i=0;i<9;i++){

        if(board[i]==""){

            board[i]=ai;
            let score=minimax(board,false);
            board[i]="";

            if(score>bestScore){
                bestScore=score;
                move=i;
            }
        }
    }

    board[move]=ai;
    createBoard();

    if(checkWin(board,ai)){
        statusText("AI Wins");
        gameOver=true;
    }
}

function minimax(board,isMax){

    if(checkWin(board,ai)) return 10;
    if(checkWin(board,human)) return -10;
    if(!board.includes("")) return 0;

    if(isMax){

        let best=-Infinity;

        for(let i=0;i<9;i++){
            if(board[i]==""){
                board[i]=ai;
                best=Math.max(best,minimax(board,false));
                board[i]="";
            }
        }

        return best;
    }

    else{

        let best=Infinity;

        for(let i=0;i<9;i++){
            if(board[i]==""){
                board[i]=human;
                best=Math.min(best,minimax(board,true));
                board[i]="";
            }
        }

        return best;
    }
}

function checkWin(b,p){

    const wins=[
        [0,1,2],[3,4,5],[6,7,8],
        [0,3,6],[1,4,7],[2,5,8],
        [0,4,8],[2,4,6]
    ];

    return wins.some(combo=>combo.every(i=>b[i]==p));
}

function statusText(text){
    document.getElementById("status").innerText=text;
}

function restart(){
    board=["","","","","","","","",""];
    gameOver=false;
    statusText("");
    createBoard();
}
