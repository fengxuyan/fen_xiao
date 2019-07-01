$(function () {
    FastClick.attach(document.body);
});

//初始化轮播图
$(".swiper-container").swiper({
    loop: true,
    autoplay: 3000
});

//图片放大浏览
$('.swiper-slide ').on('click', function () {
    var pb = $.photoBrowser({
        items: [
            "../../img/test8.jpeg",
            "../../img/test2.jpeg",
            "../../img/test3.jpeg",
        ],
        initIndex: $(this).data('initindex')
    });
    pb.open();  //打开
})

//颜色选择弹窗
$(".choose-box").on('click', function () {
    $("#choose-box").popup();
})
$(".close").on('click', function () {
    $.closePopup()
})

//加入购物车操作
$(".footer-btn .add-cart").on('click', function () {
    $("#choose-box-add").popup();

})


//颜色选择事件
$(".color-item span").on('click', function () {
    $(this).siblings().removeClass('color-choosed')
    $(this).addClass('color-choosed')
})

//分享弹出
$(".share-icon").on('click', function () {

    $.actions({
        title: '分享推荐给好友',
        actions: [{
            text: "发送给朋友",
            onClick: function () {
                //do something
            }
        }, {
            text: "生成海报",
            onClick: function () {
                $('#poster-box').css('display', 'block')
                drawcode()
                $("#poster-container").popup(
                    drawposter('../../img/test5.jpg', '../../img/test5.jpg', '由各种物质组成的巨型球状天体', '￥999.00', '使用微信扫一扫')
                )

            }
        }]
    });
})


//计数器
var MAX = 99, MIN = 1;
$('.weui-count__decrease').click(function (e) {
    var $input = $(e.currentTarget).parent().find('.weui-count__number');
    var number = parseInt($input.val() || "0") - 1
    if (number < MIN) number = MIN;
    $input.val(number)
})
$('.weui-count__increase').click(function (e) {
    var $input = $(e.currentTarget).parent().find('.weui-count__number');
    var number = parseInt($input.val() || "0") + 1
    if (number > MAX) number = MAX;
    $input.val(number)
})

//绘制海报
function drawposter(bgimg, qrcode, txt, price, des) {
    var canvas = document.getElementById('poster-box');
    var w = window.screen.availWidth * 0.7;
    var h = window.screen.availHeight * 0.55;
    $('#newimg').css({'width':w,'height':h})

    var ratio = getPixelRatio(canvas);
    var ctx = canvas.getContext('2d');

    canvas.width = w * ratio;
    canvas.height = h * ratio;
    canvas.style.width = w + 'px';
    canvas.style.height = h + 'px';

    ctx.scale(ratio, ratio);

    ctx.fillStyle="#fff";
    ctx.fillRect(0,0,w,h);

    ctx.font = "14px 微软雅黑";
    ctx.fillStyle = '#000'; // 设置颜色

    for (var i = 1; getTrueLength(txt) > 0; i++) {
        var tl = cutString(txt, 20);
        ctx.fillText(txt.substr(0, tl).replace(/^\s+|\s+$/, ""), 10, (i * 20 + h * 0.6));
        txt = txt.substr(tl);
    }
    ctx.font = "16px 微软雅黑";
    ctx.fillStyle = '#ff3b30'; // 设置颜色
    ctx.fillText(price, 10, h * 0.8)

    ctx.font = "11px 微软雅黑";
    ctx.fillStyle = '#999'; // 设置颜色
    ctx.fillText(des, w * 0.7 - 8, h * 0.6 + w * 0.4)

    var myImage = new Image();
    myImage.src = bgimg;
    myImage.crossOrigin = 'Anonymous';
    myImage.onload = function () {
        ctx.drawImage(myImage, 0, 0, w, h * 0.6);
        var myImage2 = new Image();
        myImage2.src = qrcode;
        myImage2.crossOrigin = 'Anonymous';
        myImage2.onload = function () {
            ctx.drawImage(document.getElementById("qrcodeurl"), w * 0.7 - 10, h * 0.6 + 5, w * 0.3, w * 0.3);
            $('#qrcode').hide();
            var newimg = convertCanvasToImage(canvas)
            $('#newimg').append(newimg);//imagQrDiv表示你要插入的容器id
            $('#poster-box').hide()
        }
    }
    return canvas;
}

//从 canvas 提取图片 image
function convertCanvasToImage(canvas) {
    var image = new Image();
    // 指定格式 PNG
    image.src = canvas.toDataURL("image/png");
    return image;
}

//绘制二维码
function drawcode() {
    var url = "www.baidu.com";
    jQuery('#qrcode').qrcode({
        render: "canvas",
        width: 100,     //设置宽度
        height: 100,     //设置高度
        typeNumber: -1,      //计算模式
        correctLevel: 2,
        text: url
    });
    var mycanvas1 = document.getElementsByTagName('canvas')[0]; //获取网页中的canvas对象
    //将转换后的img标签插入到html中
    var img = convertCanvasToImage(mycanvas1);
    $('#qrcode').html("");//移除已生成的避免重复生成
    $('#qrcode').append(img);//imagQrDiv表示你要插入的容器id
    $('#qrcode img').attr("id", "qrcodeurl");
}

//处理海报换行
function getTrueLength(str) { //获取字符串的真实长度（字节长度）
    var len = str.length,
        truelen = 0;
    for (var x = 0; x < len; x++) {
        if (str.charCodeAt(x) > 128) {
            truelen += 2;
        } else {
            truelen += 1;
        }
    }
    return truelen;
}

//处理海报换行
function cutString(str, leng) { //按字节长度截取字符串，返回substr截取位置
    var len = str.length,
        tlen = len,
        nlen = 0;
    for (var x = 0; x < len; x++) {
        if (str.charCodeAt(x) > 128) {
            if (nlen + 2 < leng) {
                nlen += 2;
            } else {
                tlen = x;
                break;
            }
        } else {
            if (nlen + 1 < leng) {
                nlen += 1;
            } else {
                tlen = x;
                break;
            }
        }
    }
    return tlen;
}


//模糊问题
var getPixelRatio = function (context) {
    var backingStore = context.backingStorePixelRatio ||
        context.webkitBackingStorePixelRatio ||
        context.mozBackingStorePixelRatio ||
        context.msBackingStorePixelRatio ||
        context.oBackingStorePixelRatio ||
        context.backingStorePixelRatio || 1;
    return (window.devicePixelRatio || 1) / backingStore;
};
