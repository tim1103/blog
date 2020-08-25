---
layout: post
title: 'Chrome自动操控小恐龙'
subtitle: 'Chrome小恐龙真好玩啊(雾 '
date: 2020-03-31
categories: 发现
cover: 'https://s1.ax1x.com/2020/08/11/aOw9rd.png'
tags: Chrome
---

```js
function TrexRunnerBot() {
  const makeKeyArgs = (keyCode) => {
    const preventDefault = () => void 0;
    return {keyCode, preventDefault};
  };

  const upKeyArgs = makeKeyArgs(38);
  const downKeyArgs = makeKeyArgs(40);
  const startArgs = makeKeyArgs(32);

  if (!Runner().playing) {
    Runner().onKeyDown(startArgs);
    setTimeout(() => {
      Runner().onKeyUp(startArgs);
    }, 500);
  }

  function conquerTheGame() {
    if (!Runner || !Runner().horizon.obstacles[0]) return;

    const obstacle = Runner().horizon.obstacles[0];

    if (obstacle.typeConfig && obstacle.typeConfig.type === 'SNACK') return;

    if (needsToTackle(obstacle) && closeEnoughToTackle(obstacle)) tackle(obstacle);
  }

  function needsToTackle(obstacle) {
    return obstacle.yPos !== 50;
  }

  function closeEnoughToTackle(obstacle) {
    return obstacle.xPos <= Runner().currentSpeed * 18;
  }

  function tackle(obstacle) {
    if (isDuckable(obstacle)) {
      duck();
    } else {
      jumpOver(obstacle);
    }
  }

  function isDuckable(obstacle) {
    return obstacle.yPos === 50;
  }

  function duck() {
    Runner().onKeyDown(downKeyArgs);

    setTimeout(() => {
      Runner().onKeyUp(downKeyArgs);
    }, 500);
  }

  function jumpOver(obstacle) {
    if (isNextObstacleCloseTo(obstacle))
      jumpFast();
    else
      Runner().onKeyDown(upKeyArgs);
  }

  function isNextObstacleCloseTo(currentObstacle) {
    const nextObstacle = Runner().horizon.obstacles[1];

    return nextObstacle && nextObstacle.xPos - currentObstacle.xPos <= Runner().currentSpeed * 42;
  }

  function jumpFast() {
    Runner().onKeyDown(upKeyArgs);
    Runner().onKeyUp(upKeyArgs);
  }

  return {conquerTheGame: conquerTheGame};
}

let bot = TrexRunnerBot();
let botInterval = setInterval(bot.conquerTheGame, 2);
```

食用方法:直接粘贴进 `Console` 里,按下空格,自动起跳
效果:

![](https://s1.ax1x.com/2020/08/11/aOw9rd.png)

上面的图是不小心按到了空格…恐龙站在了鸟的头上… 