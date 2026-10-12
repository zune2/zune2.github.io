
---
title: "블로그에서 즐기는 테트리스 게임"
date: 2026-10-12
categories: game
---

<div id="tetris-game-container" style="text-align: center; font-family: sans-serif; background: #202020; color: #fff; padding: 20px; border-radius: 10px; max-width: 400px; margin: 0 auto;">
    <h2>TETRIS</h2>
    <div id="score" style="font-size: 24px; margin-bottom: 10px;">SCORE: 0</div>
    <canvas id="tetris" width="240" height="400" style="border: 2px solid #fff; background-color: #000; display: block; margin: 0 auto;"></canvas>
    <button id="start-btn" style="margin-top: 15px; padding: 10px 20px; font-size: 16px; background: #3498db; color: white; border: none; border-radius: 5px; cursor: pointer;">게임 시작 / 재시작</button>
    <p style="font-size: 12px; color: #aaa; margin-top: 10px;">조작법: ← → (이동) | ↓ (가속) | ↑ (회전) | 스페이스바 (Drop)</p>
</div>

<script>
// Jekyll 마크다운 변환 시 중괄호 충돌을 방지하기 위해 일반 JS로 작성되었습니다.
const canvas = document.getElementById('tetris');
const context = canvas.getContext('2d');
const startBtn = document.getElementById('start-btn');

context.scale(20, 20);

// 라인 삭제 시 점수 계산
function arenaSweep() {
    let rowCount = 1;
    outer: for (let y = arena.length - 1; y > 0; --y) {
        for (let x = 0; x < arena[y].length; ++x) {
            if (arena[y][x] === 0) {
                continue outer;
            }
        }
        const row = arena.splice(y, 1)[0].fill(0);
        arena.unshift(row);
        ++y;
        player.score += rowCount * 10;
        rowCount *= 2;
    }
}

// 충돌 감지
function collide(arena, player) {
    const [m, o] = [player.matrix, player.pos];
    for (let y = 0; y < m.length; ++y) {
        for (let x = 0; x < m[y].length; ++x) {
            if (m[y][x] !== 0 &&
               (arena[y + o.y] &&
                arena[y + o.y][x + o.x]) !== 0) {
                return true;
            }
        }
    }
    return false;
}

// 매트릭스 생성 (보드판 및 블록용)
function createMatrix(w, h) {
    const matrix = [];
    while (h--) {
        matrix.push(new Array(w).fill(0));
    }
    return matrix;
}

// 블록 종류 생성
function createPiece(type) {
    if (type === 'I') {
        return [,
 ,
 ,
 ,
        ];
    } else if (type === 'L') {
        return [,
 ,
 ,
        ];
    } else if (type === 'J') {
        return [,
 ,
 ,
        ];
    } else if (type === 'O') {
        return [,
 ,
        ];
    } else if (type === 'Z') {
        return [,
 ,
 ,
        ];
    } else if (type === 'S') {
        return [,
 ,
 ,
        ];
    } else if (type === 'T') {
        return [,
 ,
 ,
        ];
    }
}

// 그리기 기능
function drawMatrix(matrix, offset) {
    const colors = [
        null, '#FF0D72', '#0DC2FF', '#0DFF72',
        '#F538FF', '#FF8E0D', '#FFE138', '#3877FF'
    ];
    matrix.forEach((row, y) => {
        row.forEach((value, x) => {
            if (value !== 0) {
                context.fillStyle = colors[value];
                context.fillRect(x + offset.x, y + offset.y, 1, 1);
            }
        });
    });
}

function draw() {
    context.fillStyle = '#000';
    context.fillRect(0, 0, canvas.width, canvas.height);

    drawMatrix(arena, {x: 0, y: 0});
    drawMatrix(player.matrix, player.pos);
}

// 블록 합치기
function merge(arena, player) {
    player.matrix.forEach((row, y) => {
        row.forEach((value, x) => {
            if (value !== 0) {
                arena[y + player.pos.y][x + player.pos.x] = value;
            }
        });
    });
}

// 블록 하강
function playerDrop() {
    player.pos.y++;
    if (collide(arena, player)) {
        player.pos.y--;
        merge(arena, player);
        playerReset();
        arenaSweep();
        updateScore();
    }
    dropCounter = 0;
}

// 블록 이동
function playerMove(dir) {
    player.pos.x += dir;
    if (collide(arena, player)) {
        player.pos.x -= dir;
    }
}

// 블록 리셋 (새 블록 생성)
function playerReset() {
    const pieces = 'TJLOSZI';
    player.matrix = createPiece(pieces[pieces.length * Math.random() | 0]);
    player.pos.y = 0;
    player.pos.x = (arena[0].length / 2 | 0) - (player.matrix[0].length / 2 | 0);
    if (collide(arena, player)) {
        arena.forEach(row => row.fill(0));
        alert('게임 오버! 당신의 점수: ' + player.score);
        player.score = 0;
        updateScore();
    }
}

// 블록 회전
function playerRotate(dir) {
    const pos = player.pos.x;
    let offset = 1;
    rotate(player.matrix, dir);
    while (collide(arena, player)) {
        player.pos.x += offset;
        offset = -(offset + (offset > 0 ? 1 : -1));
        if (offset > player.matrix[0].length) {
            rotate(player.matrix, -dir);
            player.pos.x = pos;
            return;
        }
    }
}

function rotate(matrix, dir) {
    for (let y = 0; y < matrix.length; ++y) {
        for (let x = 0; x < y; ++x) {
            [
                matrix[x][y],
                matrix[y][x],
            ] = [
                matrix[y][x],
                matrix[x][y],
            ];
        }
    }
    if (dir > 0) {
        matrix.forEach(row => row.reverse());
    } else {
        matrix.reverse();
    }
}

let dropCounter = 0;
let dropInterval = 1000;
let lastTime = 0;
let gameRunning = false;

function update(time = 0) {
    if (!gameRunning) return;
    const deltaTime = time - lastTime;
    lastTime = time;

    dropCounter += deltaTime;
    if (dropCounter > dropInterval) {
        playerDrop();
    }

    draw();
    requestAnimationFrame(update);
}

function updateScore() {
    document.getElementById('score').innerText = 'SCORE: ' + player.score;
}

const arena = createMatrix(12, 20);
const player = {
    pos: {x: 0, y: 0},
    matrix: null,
    score: 0,
};

// 키보드 이벤트 리스너 (블로그 스크롤 방지 포함)
window.addEventListener('keydown', event => {
    if (!gameRunning) return;
    
    if (['ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight', ' '].includes(event.key)) {
        event.preventDefault(); // 게임 중 방향키/스페이스바 누를 때 블로그 화면이 스크롤되는 것을 방지
    }

    if (event.key === 'ArrowLeft') {
        playerMove(-1);
    } else if (event.key === 'ArrowRight') {
        playerMove(1);
    } else if (event.key === 'ArrowDown') {
        playerDrop();
    } else if (event.key === 'ArrowUp') {
        playerRotate(1);
    } else if (event.key === ' ') {
        while (!collide(arena, player)) {
            player.pos.y++;
        }
        player.pos.y--;
        merge(arena, player);
        playerReset();
        arenaSweep();
        updateScore();
    }
});

// 시작 버튼 이벤트
startBtn.addEventListener('click', () => {
    arena.forEach(row => row.fill(0));
    player.score = 0;
    updateScore();
    playerReset();
    gameRunning = true;
    lastTime = performance.now();
    update();
    startBtn.blur(); // 버튼 포커스 해제하여 스페이스바 오작동 방지
});
</script>
