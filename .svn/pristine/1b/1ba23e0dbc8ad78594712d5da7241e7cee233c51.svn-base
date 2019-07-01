/**
 * 公共js
 * mail.chenc@foxmail.com
 * 2017-04-21
 */
/** 全局域名 */
var DEF_GLOBAL_DOMAIN = "http://127.0.0.1:8080/club";
//var DEF_GLOBAL_DOMAIN = "http://mp.tenglv.net";

/**
 * 跳转页面，基于windows.location.href
 * @param {Object} _url				地址
 * @param {Object} _params			参数:json格式 [{name:'name',value:'jack'}]
 */
function open_page(_url, _params){
	var _str = '';
	if(_params){
		$(_params).each(function(index,item){
			_str += '&'+item.name +'=' + encodeURI(encodeURI(item.value));
		});
		_str = _str.substr(1, _str.length - 1) + "&Rnd="+Math.random();;
	}else{
		_str += "Rnd="+Math.random();;
	}
	window.location.href = _url + "?" + _str;
}

/**
 * 添加分隔符
 * @param {Object} tip		提示语
 */
$.fn.append_divide_line = function(tip){
	if($(this).find(".divide-line").length<1){
		if(!tip){
			tip = '已经到底啦';
		}
		var divide = $('<div class="divide-line"></div>');
		divide.append('<div class="line-left"></div>');
		divide.append('<div class="info">'+tip+'</div>');
		divide.append('<div class="line-right"></div>');
		$(this).append(divide);
	}
}

/**
 * 添加空数据效果
 * @param {Object} tip
 */
$.fn.append_no_data = function(tip){
	if($(this).find(".no-data").length<1){
		if(!tip){
			tip = '暂无有效数据';
		}
		var no_data = $('<div class="no-data" style="text-align: center;margin: 3rem 0rem;"></div>');
		no_data.append('<img src="../../../../img/hotel/no-data.png" />');
		no_data.append('<div style="font-size: 0.6rem; color: #dbdbdb;">'+tip+'</div>');
		$(this).append(no_data);
	}
}

/**
 * 添加空白页
 * @param {Object} el		需要替换的dom
 * @param {Object} tip		提示语
 */
$.fn.append_empty = function(el,tip){
	var param ='<div class="empty" style="width: 100%;height: 100vh;"><img src="../../../../img/hotel/empty1.png" style="width: 9rem;height: 6rem;margin: 0 auto;display: block;margin-top: 40%;"/><p style="color: #9ea7b4;text-align: center;font-size: .65rem;">'+tip+'</p></div>';

	$(el).empty().append(param)
}



/**
 * ajax post请求,用于一般ajax请求，后台已key/value形式接收参数
 * @param {Object} url				请求地址
 * @param {Object} json_params		请求参数json格式
 * @param {Object} loading			是否展示加载提示，默认不显示
 * @param {Object} succ_callback	请求成功回调函数
 */
function ajax_post (url, json_params, loading, succ_callback, fail_callback) {
	if(loading == true){
		$.showPreloader();
	}
	if(url.indexOf("?") >= 0){
		url = url + "&Rnd="+Math.random();
	}else{
		url = url + "?Rnd="+Math.random();
	}
	$.ajax({
		url:url,
		type:'post',
		dataType:"json",
		data:json_params,
		cache: false,
		async: true,
		error: function(XMLHttpRequest, textStatus, errorThrown){
			if(loading == true){
				$.hidePreloader();
			}
			if(fail_callback){
				fail_callback();
			}
			return false;
		},
		success: function(json){
			if(succ_callback){
				succ_callback(json);
			}
			return true;
		},
		complete: function(XMLHttpRequest, textStatus){
			if(loading == true){
				$.hidePreloader();
			}
			return true;
		}
	});
}

/**
 * ajax post请求,用于一般ajax请求，后台已key/value形式接收参数
 * @param {Object} url				请求地址
 * @param {Object} json_params		请求参数json格式
 * @param {Object} loading			是否展示加载提示，默认不显示
 * @param {Object} succ_callback	请求成功回调函数
 */
function ajax_submit (url, json_params, loading, succ_callback, fail_callback) {
	if(loading == true){
		$.showPreloader();
	}
	if(url.indexOf("?") >= 0){
		url = url + "&Rnd="+Math.random();
	}else{
		url = url + "?Rnd="+Math.random();
	}
	$.ajax({
		url:url,
		type:'post',
		dataType:"json",
		contentType : 'application/json;charset=utf-8',
		data:JSON.stringify(json_params),
		cache: false,
		async: true,
		error: function(XMLHttpRequest, textStatus, errorThrown){
			if(loading == true){
				$.hidePreloader();
			}
			if(fail_callback){
				fail_callback();
			}
			return false;
		},
		success: function(json){
			if(succ_callback){
				succ_callback(json);
			}
			return true;
		},
		complete: function(XMLHttpRequest, textStatus){
			if(loading == true){
				$.hidePreloader();
			}
			return true;
		}
	});
}

/**
 * 获取URL中的参数
 * @param name			参数名
 * @returns
 */
function getURLParameter(name) {
    return unescape((new RegExp('[?|&]' + name + '=' + '([^&;]+?)(&|#|;|$)').exec(location.search)||[,""])[1].replace(/\+/g, '%20'))||null;
}


function getURLDecodeParameter(name){
    //构造一个含有目标参数的正则表达式对象  
	var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");  
	//匹配目标参数  
	var r = window.location.search.substr(1).match(reg);
	//返回参数值  
	if (r!=null) 
		return decodeURI(decodeURI(r[2]));
	return null;  
}

/**
 * 格式化金额
 * @param s	金额
 * @param n	小数点
 * @returns {String}
 */
function format_money_fen(s,n) { 
	if(!s){
		return "¥0.00";
	}else{
		s = s/100;
		if(n == 0){
			return "¥"+s; 
		}else{
			return "¥"+s.toFixed(2); 
		}
		
	}
}

/**
 * 分转元
 * @param {Object} s
 */
function fen_to_yuan(fen) { 
	if(!fen){
		return "0.00";
	}else{
		fen = fen / 100;
		return fen.toFixed(2); 
	}
}

function trim_undefined(v){
	if(v){
		return v;
	}
	return "";
}

Date.prototype.Format = function (fmt) { //author: meizz 
    var o = {
        "M+": this.getMonth() + 1, //月份 
        "d+": this.getDate(), //日 
        "h+": this.getHours(), //小时 
        "m+": this.getMinutes(), //分 
        "s+": this.getSeconds(), //秒 
        "q+": Math.floor((this.getMonth() + 3) / 3), //季度 
        "S": this.getMilliseconds() //毫秒 
    };
    if (/(y+)/.test(fmt)) {
    	fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    }
    for (var k in o){
    	if (new RegExp("(" + k + ")").test(fmt)){
    		fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ? (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    	} 
    }
    return fmt;
};

/** 日期相加天数 */
Date.prototype.dateAdd = function(strInterval, Number) {
	var dtTmp = this;
	switch (strInterval) {
	case 's' :return new Date(Date.parse(dtTmp) + (1000 * Number));
	case 'n' :return new Date(Date.parse(dtTmp) + (60000 * Number));
	case 'h' :return new Date(Date.parse(dtTmp) + (3600000 * Number));
	case 'd' :return new Date(Date.parse(dtTmp) + (86400000 * Number));
	case 'w' :return new Date(Date.parse(dtTmp) + ((86400000 * 7) * Number));
	case 'q' :return new Date(dtTmp.getFullYear(), (dtTmp.getMonth()) + Number*3, dtTmp.getDate(), dtTmp.getHours(), dtTmp.getMinutes(), dtTmp.getSeconds());
	case 'm' :return new Date(dtTmp.getFullYear(), (dtTmp.getMonth()) + Number, dtTmp.getDate(), dtTmp.getHours(), dtTmp.getMinutes(), dtTmp.getSeconds());
	case 'y' :return new Date((dtTmp.getFullYear() + Number), dtTmp.getMonth(), dtTmp.getDate(), dtTmp.getHours(), dtTmp.getMinutes(), dtTmp.getSeconds());
	}
}

/** 日期相加天数 */
Date.prototype.getWeekDay = function() {
	var day = this.getDay();
	
	switch (day) {
	case 0 :return "周日";
	case 1 :return "周一";
	case 2 :return "周二";
	case 3 :return "周三";
	case 4 :return "周四";
	case 5 :return "周五";
	case 6 :return "周六";
	}
}