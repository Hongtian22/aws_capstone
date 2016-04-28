# Hosting a Flask App on an EC2 Instance

## Step 1 - Setup Instance

Prepare EC2 instance:

* Make sure one is running.
* Make sure that you have the HTTP port, port 80, open in the Inbound security settings for your instance.
* I generally allocate an elastic IP address to these types of instances to make your life easier later on.

## Step 2 - Setup Code

Get all your stuff onto the instance. This potentially includes:

* App code.
* Python and libraries.
* ...Profit?

## Step 3 - Setup Ports

Run the following line of code at the command line on the instance:

```
sudo iptables -t nat -A PREROUTING -p tcp --dport 80 -j REDIRECT --to-ports 8000
```

This line forwards requests at port 80 to port 8000. This is important.

## Step 4 - Setup App

In the code for your app change the run method to the following:

```
app.run(host='0.0.0.0', port=8000)
```

## Step 5 - Launch App

Launch your app. I would do this in tmux, though you can use screen.

## Step 6 - Test

Test everything is working by going to the public IP address of your instance in your browser.

## Step 7

I think this is where profit goes...?
