ReverseOAuth2
===========

Another OAuth2 provider for ZF2. It provides providers for github, google and facebook others soon to come.

Usage
-----

As usual add it to your application.config.php 'ReverseOAuth2'.

Copy & rename the config/reverseoauth2.local.php.dist to your autoload folder and fill the information needed. 

### In your controller/action do:

    public function callbackAction()
    {

        $me = $this->getServiceLocator()->get('ReverseOAuth2\Google');
        //$me = $this->getServiceLocator()->get('ReverseOAuth2\Github');
        //$me = $this->getServiceLocator()->get('ReverseOAuth2\Facebook');

        if (strlen($_GET['code']) > 10) {
        	
        	if($me->getToken($this->request)) {
        		$token = $me->getSessionToken(); // token in session
        	} else {
        		$token = $me->getError(); // last returned error (array)
        	}
            
            $info = $me->getInfo();
            
        } else {
            $url = $me->getUrl();
        }

        return array('token' => $token, 'info' => $info, 'url' => $url);

    }
    
The action name depends on your settings. getUrl() will return the url where you should redirect the user, there is no automatic redirection do it yourself.


TODO
----
* Add other providers
* Write some decent documentation.
* Demo module is on it's way.