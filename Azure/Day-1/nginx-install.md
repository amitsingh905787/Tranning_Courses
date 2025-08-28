# Install and Configure Nginx on Ubuntu

## Step 1: Update Package Lists

Before installing any new software, it's a good practice to update the package lists to ensure you get the latest version.

```bash
sudo apt update
sudo apt upgrade
```

## Step 2: Install Nginx

Install Nginx using the following command:

```
sudo apt install nginx
```

## Step 3: Start Nginx Service

```
sudo systemctl start nginx
```

## Step 4: Create HTML File

```
sudo vim /var/www/html/index.html
```

Add the HTML content, for example.

```
</head>
<body>
    <h1> Welcome to nginx!</h1>
</body>
</html>
```

Save the file.

### Restart Nginx

```
sudo systemctl restart nginx
```








