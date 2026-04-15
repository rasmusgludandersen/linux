# systemd

https://systemd.io/

## [Credentials](https://systemd.io/CREDENTIALS/)
  
`LoadCredential` vs `ImportCredential`

## Example

Create cleartext password file

`echo "SuperSecretPassword" > drupal_secret.txt`

Encrypt clear text password

`systemd-creds encrypt drupal_secret.txt drupal_secret.cred --name drupal_secret`

Delete the cleartext password file

`shred -u drupal_secret.txt`

**File:** `/etc/systemd/system/php-fpm.service.d/50-password.conf`

```
[Service]
LoadCredentialEncrypted=drupal_secret:/etc/credentials/drupal_secret.cred
```

**Output:**

```bash
cat /run/credentials/php-fpm.sercice/drupal_secret
SuperSecretPassword
```

**Output:**

```bash
cat /etc/credentials/drupal_secret.cred
Whxqht+dQJax1aZeCGLxmiAAAAABAAAADAAAABAAAAA1Zhadf57dcaRd0HQAAAAAcRrgH0TPx8KDDCm
bCgFjNo7YRg5CGaeNs84gNWP09aAJ8tBfjcUBj2PHtLfAgnyFFnRvO4GnihFKZ2CWPEKT41tK5ay5M7
WO6A==
```
**File:** `current/web/sites/default/settings.environment.override.php`

```php
$cred_path = '/run/credentials/php-fpm.service/drupal_secret';
if (!is_readable($cred_path)) {
    throw new \RuntimeException("Missing Drupal secret credential: $cred_path");
}
$settings['drupal_secret'] = trim(file_get_contents($cred_path));

```
