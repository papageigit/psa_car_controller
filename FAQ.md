# FAQ 
## Frequent error
### 1. Can't get car model
The car model needs to be known by the app. To find it, the app uses the first 10 characters of your VIN.
If the car isn't in the list, we need to add it, to do that you need to edit the file here:

Go to [car_models.yml](https://github.com/flobz/psa_car_controller/blob/master/psa_car_controller/psacc/resources/car_models.yml)
and click on edit then copy an already existent model in the list and edit all properties that are incorrect for your model:
- Model
- First 10 characters of the car's VIN:  
- Usable battery capacity in kWh: [find it here](https://ev-database.org/cheatsheet/useable-battery-capacity-electric-car)
- Fuel capacity in liters
- ABRP ref: [find it here](https://api.iternio.com/1/tlm/get_carmodels_list?api_key=32b2162f-9599-4647-8139-66e9f9528370)

Finally, click on propose change. 

### 2. Error during activation {'newversion': '2.0.0', 'newversionurl': 'http://m.inwebo.com/', 'err': 'NOK:FORBIDDEN'}
Your PSA account is locked because you did 20 SMS activations. To unlock, do this: 
1. Install on a smartphone MyPeugeot, myOpel etc, depending on your car brand
2. If the application is already installed, uninstall and reinstall
3. You should be asked to give your credentials
4. Connect and test remote control, it should say that you need to reset your account
6. If the remote control works on your smartphone, it will work with psa_car_controller

### 3. No data in dashboard
The app records your position and other information if "-r" argument is provided and if data is fetched.

Data is fetched in the following scenarios:
- Charge control is enabled with "-c" program argument
- Refresh is enabled with "-R"
- You use "get_vehicleinfo" API endpoint

You need to make few trips to be able to see stats in the dashboard.

### 4. Permission error
This happens if the config file isn't writable by the user that launched the process.
To fix this, go to the application directory and execute this command:
```
# if the user is launched by pi user do
sudo chown pi: -R . 
```

### 5. I don't receive SMS
The SMS authentication is used to be able to remote control your car.
If your car doesn't have this functionality, you should disable remote control when you start psa_car_controller 
by using the `--remote-disable` argument.

### 6. SSL error
If you have an error more or less like this one:
```
[SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: self signed certificate in certificate chain (_ssl.c:1056)
```
It's a problem on PSA server so don't open an issue, you can retry a second time and if it still doesn't work you just have to wait.
You can look to issue about this problem [here](https://github.com/flobz/psa_car_controller/search?q=ssl&type=issues).

### 7. AttributeError: 'PSACarController' object has no attribute 'chc'
The setup phase didn't work. Please retry the "user config" and "otp config".

### 8. AUTHENTICATION_FAILED
One of the following parameter is incorrect:
- Email
- Password
- Country code

### 9. Lights/horn/lock doors does not work
Possible causes:
- You don't have Remote Control (not to be confused with e-Remote Control) or Connect Plus service activated for your car
- Your car does not support the features

### 10. The lights flash 10 seconds even when I input 5 seconds
This is a limitation of PSA and nothing can be done about it currently
