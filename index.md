<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<script src="https://wechatfe.github.io/vconsole/lib/vconsole.min.js?v=3.2.0"></script>
<body>
  <button id="adinfo" >getAdInfo(安卓)</button><br/><br/>
  <button id="adinfoios" >getAdInfo(ios)</button><br/><br/>
  <button id="userinfo" >getUserInfo</button><br/><br/>
  <button id="Login" >Login</button><br/><br/>
  <button id="changeMainAccount" >changeMainAccount</button><br/><br/>
  <button id="logout" >logout</button><br/><br/>
  <button id="refreshWxAccessToken" >refreshWxAccessToken</button><br/><br/>
  <button id="nativeLoginSuccess" >nativeLoginSuccess</button><br/><br/>
  <button id="invokeBonBeanPanel" >invokeBonBeanPanel</button><br/><br/>
  <button id="setTitle" >setTitle</button><br/><br/>
  <button id="openWebViewWithType" >openWebViewWithType</button><br/><br/>
  <button id="closeWebview" >closeWebview</button><br/><br/>
  <button id="gestureQuitState" >gestureQuitState</button><br/><br/>
  <button id="setGestureQuit" >setGestureQuit</button><br/><br/>
  <button id="loadRewardedAd" >loadRewardedAd</button><br/><br/>
  <button id="showRewardedAd" >showRewardedAd</button><br/><br/>
</body>
<script>

  const vconsole = new VConsole()

  const injectScript = (scriptUrl, cb) => {
    const scripts = document.createElement('script')
    scripts.type = 'text/javascript'
    scripts.src = scriptUrl
    document.getElementsByTagName('head')[0].appendChild(scripts)
    scripts.onload = () => {
      if (cb) {
        cb()
      }
    }
  }

  const getPlatform = () => {
    if (
      navigator.userAgent.toLowerCase().indexOf('iphone') > -1 ||
      navigator.userAgent.toLowerCase().indexOf('ipad') > -1
    ) {
      return 'iphone'
    } else if (navigator.userAgent.toLowerCase().indexOf('android') > -1) {
      return 'aphone'
    }
    return 'other'
  }

  const pf = getPlatform()

  const registerCallBack = () => {
    window.getAdInfoSG = (res) =>{
      console.log('getAdInfo',res)
      alert('getAdInfo',res)
    }

    window.getUserInfoSG = (res) =>{//获取登录用户信息回调
      console.log('getUserInfo',res)
      alert('getUserInfo',res)
    }

    window.LoginSG = (res) =>{//展示登录页面回调
      console.log('login',res)
      alert('login',res)
    }

    window.changeMainAccountSG = (res) =>{//切换登录账号回调
      console.log('changeMainAccount',res)
      alert('changeMainAccount',res)
    }

    window.logoutsSG = (res) =>{//退出当前登录账户回调
      console.log('logout',res)
      alert('logout',res)
    }

    window.refreshWxAccessTokenSG = (res) =>{//刷新微信accessToken回调
      console.log('refreshWxAccessToken',res)
      alert('refreshWxAccessToken',res)
    }

    window.nativeLoginSuccessSG = (res) =>{//端上登录成功通知回调
      if (res.account) {
        if (res.account === 'qq') {
          alert('qq登录') 
        } else if(res.account === 'weixin') {
          alert('微信登录') 
        }
      } else {
        alert('未登录') 
      }
    }

    window.invokeBonBeanPanelSG = (res) =>{//充值新豆面板回调
      console.log('invokeBonBeanPanel',res)
      alert('invokeBonBeanPanel',res)
    }

    window.setTitleSG = (res) =>{//设置标题回调
      console.log('setTitle',res)
      alert('setTitle',res)
    }

    window.openWebViewWithTypeSG = (res) =>{//打开新的webview回调
      console.log('openWebViewWithType',res)
      alert('openWebViewWithType',res)
    }

    window.closeWebviewSG = (res) =>{//关闭webview回调
      console.log('closeWebview',res)
      alert('closeWebview',res)
    }

    window.setGestureQuitSG = (res) =>{//禁止右滑手势回调
      console.log('setGestureQuit',res)
      alert('setGestureQuit',res)
    }

    window.loadRewardedAdSG = (res) =>{//请求激励广告回调
      console.log('loadRewardedAd',res)
      alert('loadRewardedAd',res)
    }

    window.showRewardedAdSG = (res) =>{//展示激励广告回调
      console.log('showRewardedAd',res)
      alert('showRewardedAd',res)
    }

  }
 
  const initAppData = () => {
    
  }

  window.webPageManager = {}
  window.webPageManager.pageOnShow = () =>{
    // 弹出提示&Console输出
    alert('OnShow')
  }
    
  window.webPageManager.pageOnHide = () =>{
    // 弹出提示&Console输出
    alert('OnHide')
  }

  var adinfo = document.querySelector("#adinfo")//获取用户设备相关参数(安卓)
  adinfo.onclick =()=>{
    alert(window.TencentNews.getAdInfo())
    alert(window.TencentNews.invoke('getAdInfo'))
  }

  var adinfoios = document.querySelector("#adinfoios")//获取用户设备相关参数(ios))
  adinfoios.onclick =()=>{
    window.TencentNews.invoke('getAdInfo', {'onCallback':window.getAdInfoSG})
  }

  var userinfo = document.querySelector("#userinfo")//获取登录用户信息
  userinfo.onclick =()=>{
    window.TencentNews.invoke('getUserInfo', {'onCallback':window.getUserInfoSG})
  }

  var Login = document.querySelector("#Login")//展示登录页面
  Login.onclick =()=>{
    window.TencentNews.invoke('login', {'type': 'qqorweixin','userInfo': {'id':'fakeid'},'onCallback':window.LoginSG})
  }

  var changeMainAccount = document.querySelector("#changeMainAccount")//切换登录账号
  changeMainAccount.onclick =()=>{
    window.TencentNews.invoke('changeMainAccount', {'type': 'weixin','userInfo': {'id':'fakeid'},'onCallback':window.changeMainAccountSG})
  }

  var logout = document.querySelector("#logout")//退出当前登录账户
  logout.onclick =()=>{
    window.TencentNews.invoke('logout', {'onCallback':window.logoutsSG})
  }

  var refreshWxAccessToken = document.querySelector("#refreshWxAccessToken")//刷新微信accessToken
  refreshWxAccessToken.onclick =()=>{
    window.TencentNews.invoke('refreshWxAccessToken', {'onCallback':window.refreshWxAccessTokenSG})
  }
  
  var nativeLoginSuccess = document.querySelector("#nativeLoginSuccess")//端上登录成功通知
  nativeLoginSuccess.onclick =()=>{
    window.TencentNews.invoke('getUserInfo', {'onCallback':window.nativeLoginSuccessSG})
  }

  var invokeBonBeanPanel = document.querySelector("#invokeBonBeanPanel")//充值新豆面板
  invokeBonBeanPanel.onclick =()=>{
    window.TencentNews.invoke('invokeBonBeanPanel', {
      'needBeanAmount': 300,
      'bizType':'xxx',
      'scenesId':'xxx',
      'catalogId':'xxx',
      onCallback: window.invokeBonBeanPanelSG
    })
  }

  var setTitle = document.querySelector("#setTitle")//设置标题
  setTitle.onclick =()=>{
    window.TencentNews.invoke('setTitle', {'title': '新闻腾讯','onCallback':window.setTitleSG})
  }

  var openWebViewWithType = document.querySelector("#openWebViewWithType")//打开新的webview
  openWebViewWithType.onclick =()=>{
    // window.TencentNews.invoke('openWebViewWithType', {
    //   'url': 'https://www.baidu.com/',
    //   'type': '9',
    //   'isFullScreen': 0,
    //   onCallback: window.openWebViewWithTypeSG
    // });
    window.TencentNews.openWebViewWithType('https://www.baidu.com', '9',window.openWebViewWithTypeSG)
  }

  var closeWebview = document.querySelector("#closeWebview")//关闭webview
  closeWebview.onclick =()=>{
    window.TencentNews.invoke('closeWebview', {'onCallback':window.closeWebviewSG})
  }
  
  var gesture_enable = "0" // "0":禁止 "1":不禁
  function tad_get_back_gesture_enabled() {
    return gesture_enable;
  }
  var setGestureQuit = document.querySelector("#setGestureQuit")//禁止右滑手势
  setGestureQuit.onclick =()=>{
    window.TencentNews.invoke('setGestureQuit', {'enabled':gesture_enable, 'onCallback':window.setGestureQuitSG})
  }

  loadRewardedAd.onclick =()=>{
    window.TencentNews.invoke('loadRewardedAd', {'entranceId':"abc123", 'onCallback':window.loadRewardedAdSG})
  }

  showRewardedAd.onclick =()=>{
    window.TencentNews.invoke('showRewardedAd', {'maxUnlockTime':"11", 'onCallback':window.showRewardedAdSG})
  }

  const injectAppScript = () => {
    // 新闻且安卓注入js,注入成功执行回调，回调中初始化客户端提供的数据，
    // 全局添加回调
    registerCallBack()

    if (pf === 'aphone') {
      injectScript('http://mat1.gtimg.com/www/js/newsapp/jsapi/news.js?_tsid=1', () => {
        initAppData()
      })
    }

    // TODO:新闻且iOS判断客户端初始化成功,注入成功执行回调，回调中初始化客户端提供的数据，
    if (pf === 'iphone') {
      // TencentNewsJSInjectionComplete是ios客户端提供的TencentNews注入成功的标志
      document.addEventListener('TencentNewsJSInjectionComplete', () => {
        initAppData()
      })
    }
  }

  injectAppScript()
</script>
</html>