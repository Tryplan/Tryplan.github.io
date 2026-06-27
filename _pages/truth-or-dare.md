---
permalink: /truth-or-dare/
title: "真心话 &amp; 大冒险"
layout: splash
header:
  overlay_color: "#1a0a1a"
---

<style>
  .game-container {
    min-height: 100vh;
    background: linear-gradient(135deg, #1a0a1a 0%, #2d1525 50%, #1a0a1a 100%);
    position: relative;
    overflow: hidden;
    margin: -1em -1em -1em -1em;
    padding: 0;
  }

  .page__content {
    margin: 0 !important;
    padding: 0 !important;
    max-width: 100% !important;
  }

  .hearts-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    pointer-events: none;
    overflow: hidden;
    z-index: 1;
  }

  .heart {
    position: absolute;
    top: -50px;
    color: rgba(255, 105, 135, 0.3);
    font-size: 20px;
    animation: fall linear infinite;
  }

  @keyframes fall {
    0% {
      transform: translateY(-10vh) rotate(0deg);
      opacity: 0;
    }
    10% {
      opacity: 0.6;
    }
    90% {
      opacity: 0.6;
    }
    100% {
      transform: translateY(110vh) rotate(360deg);
      opacity: 0;
    }
  }

  .game-screen {
    display: none;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
    padding: 20px;
    position: relative;
    z-index: 2;
  }

  .game-screen.active {
    display: flex;
  }

  /* Start Screen */
  .couple-names {
    text-align: center;
    margin-bottom: 60px;
  }

  .couple-names h1 {
    font-family: "STKaiti", "KaiTi", "楷体", serif;
    font-size: 3em;
    color: #fff;
    margin: 0;
    letter-spacing: 0.15em;
    text-shadow: 0 0 30px rgba(255, 105, 135, 0.5);
  }

  .heart-divider {
    display: flex;
    align-items: center;
    justify-content: center;
    margin: 20px 0;
  }

  .heart-divider::before,
  .heart-divider::after {
    content: "";
    flex: 1;
    height: 2px;
    background: linear-gradient(90deg, transparent, #ff6987, transparent);
    max-width: 80px;
  }

  .heart-divider .divider-heart {
    color: #ff6987;
    font-size: 1.5em;
    margin: 0 15px;
    animation: pulse 1.5s ease-in-out infinite;
  }

  @keyframes pulse {
    0%, 100% { transform: scale(1); }
    50% { transform: scale(1.2); }
  }

  .game-subtitle {
    text-align: center;
    color: rgba(255, 255, 255, 0.6);
    margin-bottom: 80px;
  }

  .game-subtitle .title {
    font-size: 1.5em;
    letter-spacing: 0.3em;
    margin-bottom: 10px;
    color: rgba(255, 255, 255, 0.7);
  }

  .game-subtitle .desc {
    font-size: 0.95em;
    letter-spacing: 0.1em;
    color: rgba(255, 255, 255, 0.5);
  }

  .start-btn {
    background: linear-gradient(135deg, #ff6987 0%, #e94560 100%);
    color: white;
    border: none;
    padding: 18px 80px;
    font-size: 1.3em;
    border-radius: 50px;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 8px 30px rgba(233, 69, 96, 0.4);
    letter-spacing: 0.1em;
  }

  .start-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 12px 40px rgba(233, 69, 96, 0.6);
  }

  .start-btn:active {
    transform: translateY(0);
  }

  /* Difficulty Screen */
  .difficulty-title {
    text-align: center;
    margin-bottom: 15px;
  }

  .difficulty-title h2 {
    font-size: 2.5em;
    color: #fff;
    margin: 0;
    letter-spacing: 0.15em;
    font-weight: bold;
  }

  .difficulty-subtitle {
    text-align: center;
    color: rgba(255, 255, 255, 0.5);
    font-size: 1.05em;
    margin-bottom: 50px;
    letter-spacing: 0.08em;
  }

  .difficulty-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 25px;
    max-width: 520px;
    width: 100%;
    margin-bottom: 50px;
  }

  .difficulty-card {
    background: rgba(255, 255, 255, 0.04);
    border: 2px solid rgba(255, 105, 135, 0.25);
    border-radius: 30px;
    padding: 35px 20px;
    text-align: center;
    cursor: pointer;
    transition: all 0.3s ease;
  }

  .difficulty-card:nth-child(3) {
    grid-column: 1 / -1;
    max-width: 250px;
    margin: 0 auto;
  }

  .difficulty-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
  }

  .difficulty-card.warm { border-color: rgba(255, 180, 130, 0.4); }
  .difficulty-card.warm:hover {
    border-color: rgba(255, 180, 130, 0.7);
    background: rgba(255, 180, 130, 0.08);
  }
  .difficulty-card.sweet { border-color: rgba(255, 105, 135, 0.4); }
  .difficulty-card.sweet:hover {
    border-color: rgba(255, 105, 135, 0.7);
    background: rgba(255, 105, 135, 0.08);
  }
  .difficulty-card.spicy { border-color: rgba(255, 60, 90, 0.5); }
  .difficulty-card.spicy:hover {
    border-color: rgba(255, 60, 90, 0.8);
    background: rgba(255, 60, 90, 0.1);
  }

  .difficulty-icon {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    margin: 0 auto 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
  }

  .difficulty-card.warm .difficulty-icon {
    background: linear-gradient(135deg, rgba(255, 180, 130, 0.3), rgba(255, 150, 100, 0.15));
  }
  .difficulty-card.sweet .difficulty-icon {
    background: linear-gradient(135deg, rgba(255, 105, 135, 0.3), rgba(255, 80, 120, 0.15));
  }
  .difficulty-card.spicy .difficulty-icon {
    background: linear-gradient(135deg, rgba(255, 60, 90, 0.35), rgba(220, 40, 70, 0.15));
  }

  .difficulty-name {
    font-size: 1.6em;
    font-weight: bold;
    margin-bottom: 10px;
    letter-spacing: 0.1em;
  }

  .difficulty-card.warm .difficulty-name { color: #ffb482; }
  .difficulty-card.sweet .difficulty-name { color: #ff6987; }
  .difficulty-card.spicy .difficulty-name { color: #ff3c5a; }

  .difficulty-desc {
    color: rgba(255, 255, 255, 0.6);
    font-size: 0.9em;
    line-height: 1.6;
  }

  .difficulty-desc .line1 { margin-bottom: 5px; }

  .back-btn {
    background: transparent;
    color: #ff6987;
    border: 2px solid rgba(255, 105, 135, 0.5);
    padding: 14px 60px;
    font-size: 1em;
    border-radius: 50px;
    cursor: pointer;
    transition: all 0.3s ease;
    letter-spacing: 0.1em;
  }

  .back-btn:hover {
    background: rgba(255, 105, 135, 0.1);
    border-color: #ff6987;
  }

  /* Game Screen */
  .game-header {
    width: 100%;
    max-width: 500px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 30px;
  }

  .round-info {
    background: rgba(255, 255, 255, 0.08);
    padding: 12px 28px;
    border-radius: 30px;
    color: rgba(255, 255, 255, 0.6);
    font-size: 1.1em;
    letter-spacing: 0.05em;
  }

  .difficulty-badge {
    position: absolute;
    top: 20px;
    right: 20px;
    background: rgba(255, 105, 135, 0.15);
    border: 1px solid rgba(255, 105, 135, 0.3);
    padding: 8px 16px;
    border-radius: 20px;
    color: #ff8fa3;
    font-size: 0.85em;
  }

  .restart-btn {
    background: rgba(255, 255, 255, 0.1);
    border: none;
    width: 45px;
    height: 45px;
    border-radius: 50%;
    color: rgba(255, 255, 255, 0.7);
    cursor: pointer;
    font-size: 1.2em;
    transition: all 0.3s ease;
  }

  .restart-btn:hover {
    background: rgba(255, 255, 255, 0.2);
    color: #fff;
  }

  /* Players Bar - pill style */
  .players-bar {
    width: 100%;
    max-width: 500px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 35px;
  }

  .player-card {
    flex: 1;
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 12px 18px;
    background: rgba(255, 255, 255, 0.05);
    border-radius: 50px;
    border: 2px solid transparent;
    transition: all 0.3s ease;
    position: relative;
  }

  .player-card.active {
    border-color: #ff6987;
    background: rgba(255, 105, 135, 0.12);
    box-shadow: 0 0 20px rgba(255, 105, 135, 0.25);
  }

  .player-avatar {
    width: 52px;
    height: 52px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: white;
    font-size: 1.35em;
    font-weight: bold;
    flex-shrink: 0;
  }

  .player-card[data-player="wxb"] .player-avatar {
    background: linear-gradient(135deg, #5ba0e8 0%, #3a7bc7 100%);
  }

  .player-card[data-player="yst"] .player-avatar {
    background: linear-gradient(135deg, #ff7a93 0%, #ed5572 100%);
  }

  .player-info {
    flex: 1;
  }

  .player-name {
    color: #fff;
    font-size: 1.05em;
    margin-bottom: 2px;
    line-height: 1.3;
  }

  .player-score {
    color: #ffd700;
    font-size: 1.25em;
    font-weight: bold;
    position: absolute;
    right: 20px;
    top: 50%;
    transform: translateY(-50%);
  }

  .vs-text {
    color: rgba(255, 255, 255, 0.4);
    font-size: 1.2em;
    margin: 0 15px;
    font-weight: bold;
  }

  .turn-indicator {
    text-align: center;
    margin-bottom: 25px;
    color: rgba(255, 255, 255, 0.6);
    font-size: 1.2em;
  }

  .turn-indicator .current-player {
    color: #ff6987;
    font-weight: bold;
  }

  /* Main Card - the big center card */
  .main-card {
    width: 100%;
    max-width: 500px;
    background: rgba(255, 255, 255, 0.04);
    backdrop-filter: blur(10px);
    border: 2px solid rgba(255, 105, 135, 0.25);
    border-radius: 35px;
    padding: 70px 30px;
    text-align: center;
    margin-bottom: 35px;
    min-height: 320px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    transition: all 0.4s ease;
  }

  .main-card.has-question {
    border-color: rgba(255, 105, 135, 0.4);
  }

  .card-prompt {
    color: rgba(255, 255, 255, 0.5);
    font-size: 1.4em;
    margin-bottom: 15px;
    letter-spacing: 0.05em;
  }

  .card-hint {
    color: rgba(255, 255, 255, 0.35);
    font-size: 1em;
    letter-spacing: 0.03em;
  }

  .question-type-badge {
    display: inline-block;
    background: rgba(255, 105, 135, 0.2);
    color: #ff8fa3;
    padding: 10px 28px;
    border-radius: 30px;
    font-size: 1em;
    margin-bottom: 30px;
    letter-spacing: 0.05em;
  }

  .question-text {
    color: #fff;
    font-size: 1.5em;
    line-height: 1.6;
    letter-spacing: 0.03em;
    font-weight: 500;
  }

  /* Bottom action buttons */
  .action-row {
    display: flex;
    gap: 25px;
    width: 100%;
    max-width: 500px;
    margin-bottom: 25px;
  }

  .pill-btn {
    flex: 1;
    padding: 18px 20px;
    border: 2px solid;
    border-radius: 50px;
    font-size: 1.3em;
    cursor: pointer;
    transition: all 0.3s ease;
    letter-spacing: 0.08em;
    background: rgba(255, 255, 255, 0.04);
    font-weight: 500;
  }

  .pill-btn.truth {
    color: #ff6987;
    border-color: rgba(255, 105, 135, 0.5);
    background: linear-gradient(135deg, rgba(255, 105, 135, 0.1), rgba(255, 105, 135, 0.02));
  }

  .pill-btn.truth:hover {
    background: rgba(255, 105, 135, 0.15);
    border-color: #ff6987;
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(255, 105, 135, 0.3);
  }

  .pill-btn.dare {
    color: #ffb482;
    border-color: rgba(255, 180, 130, 0.5);
    background: linear-gradient(135deg, rgba(255, 180, 130, 0.1), rgba(255, 180, 130, 0.02));
  }

  .pill-btn.dare:hover {
    background: rgba(255, 180, 130, 0.15);
    border-color: #ffb482;
    transform: translateY(-2px);
    box-shadow: 0 8px 25px rgba(255, 180, 130, 0.3);
  }

  .answer-row {
    display: flex;
    flex-direction: column;
    gap: 15px;
    width: 100%;
    max-width: 400px;
    margin-bottom: 25px;
  }

  .complete-btn {
    background: linear-gradient(135deg, #ff6987 0%, #e94560 100%);
    color: white;
    border: none;
    padding: 18px 40px;
    font-size: 1.15em;
    border-radius: 50px;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 6px 25px rgba(233, 69, 96, 0.35);
    letter-spacing: 0.05em;
  }

  .complete-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 10px 35px rgba(233, 69, 96, 0.5);
  }

  .skip-btn {
    background: transparent;
    color: rgba(255, 215, 0, 0.7);
    border: 2px solid rgba(255, 215, 0, 0.4);
    padding: 16px 40px;
    font-size: 1em;
    border-radius: 50px;
    cursor: pointer;
    transition: all 0.3s ease;
    letter-spacing: 0.05em;
  }

  .skip-btn:hover {
    background: rgba(255, 215, 0, 0.1);
    border-color: #ffd700;
    color: #ffd700;
  }

  .back-to-menu {
    color: rgba(255, 255, 255, 0.4);
    font-size: 0.95em;
    cursor: pointer;
    transition: color 0.3s ease;
    background: none;
    border: none;
    letter-spacing: 0.05em;
  }

  .back-to-menu:hover {
    color: rgba(255, 255, 255, 0.7);
  }

  @media (max-width: 480px) {
    .couple-names h1 { font-size: 2.2em; }
    .difficulty-title h2 { font-size: 2em; }
    .difficulty-grid { gap: 18px; }
    .difficulty-card { padding: 25px 15px; }
    .difficulty-icon { width: 60px; height: 60px; font-size: 1.5em; }
    .difficulty-name { font-size: 1.3em; }
    .question-text { font-size: 1.2em; }
    .start-btn { padding: 16px 60px; font-size: 1.1em; }
    .main-card { padding: 50px 20px; min-height: 280px; }
    .card-prompt { font-size: 1.2em; }
    .pill-btn { font-size: 1.15em; padding: 16px 15px; }
    .player-name { font-size: 0.95em; }
    .player-avatar { width: 45px; height: 45px; font-size: 1.2em; }
  }
</style>

<div class="game-container">
  <div class="hearts-container" id="heartsContainer"></div>

  <!-- Start Screen -->
  <div class="game-screen active" id="startScreen">
    <div class="couple-names">
      <h1>WXB</h1>
      <div class="heart-divider">
        <span class="divider-heart">❤</span>
      </div>
      <h1>YST</h1>
    </div>
    <div class="game-subtitle">
      <div class="title">真心话大冒险</div>
      <div class="desc">属于你们两个人的浪漫小游戏</div>
    </div>
    <button class="start-btn" onclick="showDifficultyScreen()">▶ 开始游戏</button>
  </div>

  <!-- Difficulty Screen -->
  <div class="game-screen" id="difficultyScreen">
    <div class="difficulty-title">
      <h2>选择难度</h2>
    </div>
    <div class="difficulty-subtitle">不同的难度，不同的心跳</div>
    <div class="difficulty-grid">
      <div class="difficulty-card warm" onclick="selectDifficulty('warm')">
        <div class="difficulty-icon">☀️</div>
        <div class="difficulty-name">温馨</div>
        <div class="difficulty-desc">
          <div class="line1">暖暖的日常</div>
          <div>适合刚刚开始</div>
        </div>
      </div>
      <div class="difficulty-card sweet" onclick="selectDifficulty('sweet')">
        <div class="difficulty-icon">💖</div>
        <div class="difficulty-name">甜蜜</div>
        <div class="difficulty-desc">
          <div class="line1">心动加速</div>
          <div>适合热恋中的你们</div>
        </div>
      </div>
      <div class="difficulty-card spicy" onclick="selectDifficulty('spicy')">
        <div class="difficulty-icon">🔥</div>
        <div class="difficulty-name">火辣</div>
        <div class="difficulty-desc">
          <div class="line1">脸红心跳</div>
          <div>准备好了再选</div>
        </div>
      </div>
    </div>
    <button class="back-btn" onclick="backToStart()">返回</button>
  </div>

  <!-- Game Screen -->
  <div class="game-screen" id="gameScreen">
    <div class="game-header">
      <div class="round-info">第 <span id="roundNum">1</span> 轮</div>
      <button class="restart-btn" onclick="restartGame()" title="重新开始">↻</button>
    </div>
    <div class="players-bar">
      <div class="player-card" data-player="wxb" id="playerWxb">
        <div class="player-avatar">W</div>
        <div class="player-info">
          <div class="player-name">WXB</div>
        </div>
        <div class="player-score" id="scoreWxb">0</div>
      </div>
      <span class="vs-text">VS</span>
      <div class="player-card" data-player="yst" id="playerYst">
        <div class="player-avatar">Y</div>
        <div class="player-info">
          <div class="player-name">YST</div>
        </div>
        <div class="player-score" id="scoreYst">0</div>
      </div>
    </div>
    <div class="turn-indicator">
      轮到 <span class="current-player" id="currentPlayerName">WXB</span> 选择
    </div>
    <div class="main-card" id="mainCard">
      <div class="card-prompt" id="cardPrompt">选择真心话或大冒险</div>
      <div class="card-hint" id="cardHint">点击下方按钮抽取题目</div>
    </div>
    <div class="action-row" id="choiceRow">
      <button class="pill-btn truth" onclick="showQuestion('truth')">真心话</button>
      <button class="pill-btn dare" onclick="showQuestion('dare')">大冒险</button>
    </div>
    <div class="answer-row" id="answerRow" style="display:none;">
      <button class="complete-btn" onclick="completeChallenge()">✓ 完成挑战</button>
      <button class="skip-btn" onclick="skipChallenge()">⏭ 跳过（接受惩罚）</button>
    </div>
    <button class="back-to-menu" onclick="backToMenu()">返回主菜单</button>
  </div>
</div>

<script>
  const questionBank = {
    warm: {
      truth: [
        "第一次见面时，你对我的第一印象是什么？",
        "你最喜欢的季节是什么？为什么？",
        "你最喜欢吃什么菜？",
        "你最想去的旅游目的地是哪里？",
        "你平时有什么兴趣爱好？",
        "你觉得自己最大的优点是什么？",
        "你最欣赏我的什么特质？",
        "你的生日是哪天？你喜欢怎么过生日？",
        "你最喜欢的电影是哪一部？",
        "你最近在追什么剧或综艺？",
        "你最喜欢的一首歌是什么？",
        "你小时候的梦想是什么？",
        "你觉得一天中最美好的时刻是什么时候？",
        "你最喜欢的动物是什么？养过宠物吗？",
        "你最难忘的一次生日是怎样的？",
        "你最喜欢的颜色是什么？为什么？",
        "你平时周末一般怎么安排？",
        "你喜欢什么类型的电影？",
        "你最想学会的一项技能是什么？",
        "你觉得朋友最重要的品质是什么？"
      ],
      dare: [
        "唱一首你最喜欢的歌的副歌部分",
        "学猫叫三声，还要配合动作",
        "做一个可爱的表情包，让对方拍下来",
        "模仿一种动物的叫声和动作",
        "用普通话、粤语、英语各说一句「你好」",
        "表演一个抖音热门舞蹈片段",
        "做20个深蹲",
        "用左手/右手写字，写对方的名字",
        "模仿机器人说话30秒",
        "讲一个冷笑话，对方笑了才算过",
        "单脚站立10秒，不能晃",
        "用最嗲的声音说「我好喜欢你呀」",
        "做鬼脸，保持5秒不许笑",
        "即兴表演一段天气预报",
        "用三种不同的语气说「今天天气真好」",
        "模仿你最喜欢的动漫角色说一句台词",
        "做10个俯卧撑",
        "原地转5圈，然后走直线",
        "模仿老师上课的样子",
        "对镜头做一个飞吻的动作"
      ]
    },
    sweet: {
      truth: [
        "我们是哪一天正式在一起的？还记得具体细节吗？",
        "你是从什么时候开始喜欢上我的？",
        "第一次约会你紧张吗？心里在想什么？",
        "第一次牵手/拥抱是什么感觉？",
        "和我在一起后，你觉得自己最大的变化是什么？",
        "你最喜欢我身上的哪个优点？",
        "你最受不了我的哪个小毛病？",
        "我们在一起后，最让你感动的一件事是什么？",
        "你有没有偷偷生过我的气？因为什么？",
        "你觉得我们最默契的时刻是什么？",
        "你最想和我一起做但还没做的事是什么？",
        "如果只能选一个，你最想和我去哪个地方旅行？",
        "你对我们的未来有什么期待或担心？",
        "你觉得我最大的魅力是什么？",
        "如果我惹你生气了，你希望我怎么哄你？",
        "你觉得我们之间最浪漫的瞬间是什么？",
        "你最想和我一起养什么宠物？",
        "你觉得我们的爱情保鲜秘诀是什么？",
        "你最喜欢我怎么称呼你？",
        "你最想收到我送的什么礼物？",
        "你觉得我们在一起最开心的事情是什么？",
        "你会不会经常想起我？在什么时候？",
        "你最喜欢我穿什么风格的衣服？",
        "你觉得我做什么事情的时候最可爱？",
        "如果有一天我不在你身边，你最想我什么？",
        "你觉得爱情里最重要的是什么？",
        "你最害怕失去什么？",
        "你人生中最大的梦想是什么？我在里面吗？",
        "你觉得我最需要被理解的地方是什么？",
        "你有没有什么话一直想对我说但没说出口？"
      ],
      dare: [
        "对我深情告白30秒，不许笑",
        "用五种不同的语言说「我爱你」",
        "模仿我平时生气的样子",
        "公主抱/背我走十步",
        "画一幅我的肖像画（限时1分钟）",
        "给我唱一首情歌，要完整唱完副歌",
        "给对方按摩肩膀5分钟",
        "用最嗲的声音说「老公/老婆我错了」",
        "给我写一句情话，念出来",
        "用三种不同的语气说「我喜欢你」",
        "亲一下我的额头/脸颊/手背（选一个）",
        "对我做一个爱心手势并眨眼",
        "给我一个大大的拥抱，持续10秒",
        "说我的10个优点，限时30秒",
        "背诵我们的纪念日（在一起的日子、生日...）",
        "模仿我平时撒娇的样子",
        "猜我现在心里在想什么",
        "模仿我平时吃醋的样子",
        "喂我吃一口东西",
        "和我自拍一张亲密合照",
        "从背后抱住我，在耳边说一句悄悄话",
        "牵起我的手，深情对视10秒",
        "给我讲一个睡前小故事",
        "帮我整理一下头发/衣服",
        "用鼻子轻轻碰一下我的鼻子",
        "对我说一句只有我们俩懂的暗号",
        "给我比一个大大的爱心",
        "轻轻摸一下我的头",
        "和我十指相扣，说一句甜言蜜语",
        "在我耳边轻轻说「我喜欢你」"
      ]
    },
    spicy: {
      truth: [
        "你理想中的求婚方式是什么样的？",
        "如果时光可以倒流，你想回到我们的哪一天？",
        "如果对方突然消失24小时，你会怎么做？",
        "你觉得我们之间最需要改进的是什么？",
        "如果有一天我们吵架了，你会怎么哄我？",
        "你最害怕失去什么？",
        "你人生中最大的梦想是什么？我在里面吗？",
        "你觉得我最需要被理解的地方是什么？",
        "你有没有什么话一直想对我说但没说出口？",
        "如果有一天我变老了变丑了，你还会爱我吗？",
        "你觉得我们的关系里，你付出最多的是什么？",
        "你有没有对我撒过谎？是什么事？",
        "你觉得我做过最让你失望的事是什么？",
        "如果我们之间有100步，你愿意走多少步？",
        "你想过和我结婚吗？从什么时候开始想的？",
        "你觉得我们能在一起多久？",
        "如果有一天我要离开这座城市，你会跟我走吗？",
        "你最想和我一起住什么样的房子？",
        "你觉得我们以后会有几个孩子？",
        "你最想和我一起过怎样的生活？",
        "如果只能选择一个，你选你爱的人还是爱你的人？",
        "你觉得爱情和面包哪个更重要？",
        "你有没有想象过我们的婚礼是什么样的？",
        "你最想在什么地方和我一起看日出/日落？",
        "你觉得我是你的理想型吗？哪里最符合？",
        "如果有一天我们分手了，你最舍不得的是什么？",
        "你最想带我去见你的谁？为什么？",
        "你觉得我在你心里排第几？",
        "如果我生病了需要人照顾，你会怎么做？",
        "你最想对我说的一句话是什么？"
      ],
      dare: [
        "深情对视30秒，谁先笑谁输",
        "公主抱我做5个深蹲",
        "用嘴解开我衣服上的一颗扣子（任选）",
        "在我脖子上种一颗草莓",
        "壁咚我，说一句霸道总裁的台词",
        "把我抱起来坐在你腿上",
        "用舌头舔掉对方嘴角的东西",
        "法式接吻10秒",
        "从背后抱住我，手放在我腰上",
        "把我按在墙上，亲我的脖子",
        "坐在我腿上，说10句撩我的话",
        "摸我的脸，慢慢靠近，最后亲一下",
        "背对着我坐下，我抱着你，持续30秒",
        "把我横抱起来，走到房间另一头",
        "用手指轻轻划过我的嘴唇",
        "在我耳边吹气，说一句悄悄话",
        "把我拉进怀里，紧紧抱着我",
        "亲我的锁骨",
        "让我坐在你腿上，你抱着我摇",
        "用嘴巴喂我喝水/饮料",
        "脱掉对方一件衣服（外搭即可）",
        "蒙着眼睛亲对方的脸，猜亲到的是哪里",
        "两人十指相扣，深情说情话",
        "把我推到床上，趴在我身上10秒",
        "挠我痒痒，直到我求饶",
        "给我来一个偶像剧式的壁咚",
        "抱着我转三圈，然后稳稳放下",
        "用你的外套把我裹在怀里",
        "在人群中偷偷牵我的手，十指相扣",
        "下雨天把伞全偏向我，自己淋湿半边"
      ]
    }
  };

  const difficultyNames = {
    warm: "☀️ 温馨",
    sweet: "💖 甜蜜",
    spicy: "🔥 火辣"
  };

  let currentPlayer = "wxb";
  let currentRound = 1;
  let scores = { wxb: 0, yst: 0 };
  let currentDifficulty = "sweet";
  let usedQuestions = { warm: {}, sweet: {}, spicy: {} };
  let showingQuestion = false;

  const playerNames = {
    wxb: "WXB",
    yst: "YST"
  };

  function createHearts() {
    const container = document.getElementById("heartsContainer");
    const hearts = ["❤", "💕", "💗", "💖", "💝", "♥"];
    for (let i = 0; i < 25; i++) {
      const heart = document.createElement("div");
      heart.className = "heart";
      heart.textContent = hearts[Math.floor(Math.random() * hearts.length)];
      heart.style.left = Math.random() * 100 + "%";
      heart.style.animationDuration = (Math.random() * 10 + 8) + "s";
      heart.style.animationDelay = (Math.random() * 10) + "s";
      heart.style.fontSize = (Math.random() * 15 + 12) + "px";
      heart.style.opacity = Math.random() * 0.4 + 0.1;
      container.appendChild(heart);
    }
  }

  function showDifficultyScreen() {
    showScreen("difficultyScreen");
  }

  function backToStart() {
    showScreen("startScreen");
  }

  function selectDifficulty(difficulty) {
    currentDifficulty = difficulty;
    startGame();
  }

  function startGame() {
    currentPlayer = "wxb";
    currentRound = 1;
    scores = { wxb: 0, yst: 0 };
    usedQuestions = { warm: {}, sweet: {}, spicy: {} };
    showingQuestion = false;
    resetCard();
    showScreen("gameScreen");
    updateUI();
  }

  function showScreen(screenId) {
    document.querySelectorAll(".game-screen").forEach(s => s.classList.remove("active"));
    document.getElementById(screenId).classList.add("active");
  }

  function updateUI() {
    document.getElementById("roundNum").textContent = currentRound;
    document.getElementById("scoreWxb").textContent = scores.wxb;
    document.getElementById("scoreYst").textContent = scores.yst;
    document.getElementById("currentPlayerName").textContent = playerNames[currentPlayer];

    document.querySelectorAll(".player-card").forEach(card => {
      card.classList.remove("active");
      if (card.getAttribute("data-player") === currentPlayer) {
        card.classList.add("active");
      }
    });
  }

  function resetCard() {
    const card = document.getElementById("mainCard");
    card.classList.remove("has-question");
    card.innerHTML = `
      <div class="card-prompt" id="cardPrompt">选择真心话或大冒险</div>
      <div class="card-hint" id="cardHint">点击下方按钮抽取题目</div>
    `;
    document.getElementById("choiceRow").style.display = "flex";
    document.getElementById("answerRow").style.display = "none";
  }

  function showQuestion(type) {
    let questions = questionBank[currentDifficulty][type];
    if (!usedQuestions[currentDifficulty][type]) {
      usedQuestions[currentDifficulty][type] = [];
    }
    let used = usedQuestions[currentDifficulty][type];

    if (used.length >= questions.length) {
      usedQuestions[currentDifficulty][type] = [];
      used = [];
    }

    let available = questions.filter((_, i) => !used.includes(i));
    let randomIndex = Math.floor(Math.random() * available.length);
    let actualIndex = questions.indexOf(available[randomIndex]);

    used.push(actualIndex);

    const typeLabel = type === "truth" ? "💬 真心话" : "😜 大冒险";
    const card = document.getElementById("mainCard");
    card.classList.add("has-question");
    card.innerHTML = `
      <span class="question-type-badge">${typeLabel}</span>
      <div class="question-text">${available[randomIndex]}</div>
    `;

    document.getElementById("choiceRow").style.display = "none";
    document.getElementById("answerRow").style.display = "flex";
    showingQuestion = true;
  }

  function completeChallenge() {
    scores[currentPlayer] += 1;
    nextTurn();
  }

  function skipChallenge() {
    nextTurn();
  }

  function nextTurn() {
    currentPlayer = currentPlayer === "wxb" ? "yst" : "wxb";
    if (currentPlayer === "wxb") {
      currentRound++;
    }
    resetCard();
    updateUI();
  }

  function restartGame() {
    if (confirm("确定要重新开始游戏吗？")) {
      showDifficultyScreen();
    }
  }

  function backToMenu() {
    if (confirm("确定要返回主菜单吗？当前进度将丢失。")) {
      showScreen("startScreen");
    }
  }

  createHearts();
</script>
