可以从phaser的github库（https://github.com/photonstorm/phaser-examples）得到示例代码。

phaser只需要浏览器支持canvas标签即可工作。

phaser的基础框架

    var game = new Phaser.Game(800, 600, Phaser.AUTO, '', { preload: preload, create: create, update: update });
    # 前两个参数是定义canvas的宽度和高度（800*600像素）
    # 第三个参数是渲染环境，可选CANVAS,WEBGL,AUTO（推荐，会优先使用WEBGL）.   
    # 第四个参数是一个代表HTML DOM的ID字符，在哪个标签下创建canvas，默认在body下。
    
    function preload() {
    }

    function create() {
    }

    function update() {
    }
    
phaser自适应窗口，在preload中加载

    game.scale.scaleMode = Phaser.ScaleManager.SHOW_ALL;
    game.scale.pageAlignHorizontally = true;
    game.scale.pageAlignVertically = true;
    
用bitmapdata创建sprite，在create中

    var bmd = game.add.bitmapData(24, 24);
    bmd.context.arc(12, 12, 12, 0, 2 * Math.PI);
    bmd.context.fillStyle = 'orange';
    bmd.context.fill();
    game.cache.addBitmapData('circle', bmd);
    
    sprite = game.add.sprite(400, 300, game.cache.getBitmapData('circle'));
    sprite.anchor.setTo(0.5, 0.5);
    sprite.tint = Phaser.Color.ORANGE;    
    
对sprite开启物理引擎

    game.physics.startSystem(Phaser.Physics.ARCADE);
    game.physics.arcade.enable([sprite, sprite1]);
    sprite.body.setCircle(12);  // 用圆做边缘检测
    sprite1.body.setCircle(12);
    sprite.body.bounce.set(1); // 碰撞后速度返还100%
    sprite1.body.bounce.set(1);
    sprite1.body.immovable = true; // 该精灵被撞无法移动
    

    