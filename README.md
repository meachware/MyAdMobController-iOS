# MyAdMobController-iOS
Cocos2d/Spritebuilder AdMob controller for iOS

IMPORTANT! This controller works only with iOS and AdMob iOS SDK. If you develop for android use #if __CC_PLATFORM_IOS for it methods. Also dont add it files to Android target.

HowTo use.

Download AdMob iOS SDK and add it to your project https://developers.google.com/mobile-ads-sdk/download

At first you need to load ad. I recommend do it on AppDelegate:

  [[MyAdMobController sharedController] loadBannerView];
  
  [[MyAdMobController sharedController] loadInterstitial];
  
Then load ad from your scene.

For load Interstitial on current scene just call this methods on - (void)onEnter

  UIViewController *rootViewController = [[[[UIApplication sharedApplication] delegate] window] rootViewController];
  [[MyAdMobController sharedController] showInterstitialOnViewController:rootViewController];
  
  
For show BannerView first create UIView and add it to top of root UIView:

  UIView *adView = [[UIView alloc] initWithFrame:adRect];
  [[CCDirector sharedDirector].view addSubview:adView];
  
then add Banner View to it:

  [[MyAdMobController sharedController] addBannerToView:adView];
  
If you need to resolve some controller methods on your scene use <MyAdMobControllerDelagate> protocol:

  @interface MyScene () <MyAdMobControllerDelagate>

then set delegate:

  [[MyAdMobController sharedController] setDelegate:self];
  
and implement this methods on your scene implementation:

  - (void)MyInterstitialDidDismissScreen:(GADInterstitial *)ad;
  - (void)MyInterstitial:(GADInterstitial *)ad didFailToReceiveAdWithError:(GADRequestError *)error;
  - (void)MyAdViewDidReceiveAd:(GADBannerView *)view;
  - (void)MyAdView:(GADBannerView *)view didFailToReceiveAdWithError:(GADRequestError *)error;

  