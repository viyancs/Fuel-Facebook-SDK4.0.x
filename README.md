Fuel-Facebook-SDK4.0.x
======================

This is Facebook Package for installed on Fuelphp package class


Instalation
---------
<ol>
   <li> Copy this package under directory /fuel/packages </li>
   <li> Then Open config.php give facebook packages auto load </li>
   <pre>
   'packages'  => array(
		 	                  'orm',
                        'parser',
                        'email',
                        'facebook'
		 ),
   </pre>
</ol>

Usage Tab Apps with authentication
-----
Tab apps page usage when you want to build custom application under your tab of page, and with this code you can authenticated to get Session of user is logged by facebook, and then process that session by your self for more complex method and action.
<pre>
        // start session
        if (session_status() == PHP_SESSION_NONE) session_start();
        \Facebook\FacebookSession::setDefaultApplication(\Config::get('main.app_id'), \Config::get('main.secret_id'));
        $page_helper = new \Facebook\FacebookPageTabHelper();
        $helper = new \Facebook\FacebookRedirectLoginHelper(\Config::get('main.redirect_url'));

        try {
            $session = $page_helper->getSession();
        } catch (\Facebook\FacebookRequestException $e) {
            var_dump($e);exit;
        } catch (\Exception $e) {
            // Some other error occurred
            var_dump($e);exit;
        }

        if (empty($session)) {
            $params = array('email', 'user_friends','public_profile');
            $auth_url = $helper->getLoginUrl($params);
            printf('Redirecting to Facebook authentication page, please wait...<script>top.location.href = \'%s\';</script>', $auth_url);
            exit;
        } 
            
        // create a session using saved token or the new one we generated at login
        $session = new \Facebook\FacebookSession($session->getToken());
        var_dump($session)
</pre>

Reference
---------
Repo [Facebook SDK 4.0](https://github.com/facebook/facebook-php-sdk-v4) <br/>
about [Page Tab] (https://developers.facebook.com/docs/appsonfacebook/pagetabs)<br/>
about [Login Flow](https://developers.facebook.com/docs/facebook-login/manually-build-a-login-flow/v2.1)<br/>
