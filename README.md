# Use ddev with Sage

This is how I work with ddev + Bedrock + Acorn + Sage.

[DDEV](https://ddev.com/) - [Roots](https://roots.io/)


```
cd your-project/
ddev config --project-type=wordpress --docroot=web
```

Edit .ddev/config.yaml and add :

```
web_extra_exposed_ports:
  - name: bud
    container_port: 3000
    http_port: 3000
    https_port: 3001
```
 
Run `ddev start`
 
Edit `.env` :
 
```
WP_HOME='http://project.ddev.site'
WP_SITEURL="${WP_HOME}/wp"
```
  
Edit `web/app/themes/sage/bud.config.[m]js` :
 
```
/**
 * Development origin
 * @see {@link https://bud.js.org/docs/bud.serve/}
 */
.serve(3000)

/**
 * Proxy origin (`WP_HOME`)
 * @see {@link https://bud.js.org/docs/bud.proxy/}
 */
.proxy('http://project.ddev.site')

/**
 * URI of the `public` directory
 * @see {@link https://bud.js.org/docs/bud.setPublicPath/}
 */
.setPublicPath('/app/themes/sage/public/')

/**
 * Used to specify the site-accessible URL for the dev server.
 * @see {@link https://bud.js.org/docs/bud.setPublicUrl/}
 */
.setPublicUrl('http://project.ddev.site:3000');
```
 
 
