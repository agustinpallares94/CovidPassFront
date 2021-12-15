![CovidPass](https://covidpass.marvinsextro.de/thumbnail.png)

Web App que permite generar tu certificado covid digital a partir del PDF de vacunación.


## Running it yourself

Es necesario utilizar tus propios certificados para la API .NET así como definir los campos de idenficador de equipo en el front.

### Deploy the web app

Es necesario definir un archivo .env donde definas la url de la api a la cual va a mandar el pkpass para que se firme. Se ha utlizado este código https://github.com/covidpass-org/covidpass

```sh
yarn build
yarn start
```

```

### Deploy the API

Tienes que definir en el código los certificados propios de tu equipo. Se ha utilizado este código https://github.com/covidpass-org/CovidPassApiNet .
Desde visual code puede ejecutarlo o sino:

```sh
dotnet build
dotnet run
```

## Get your certificate

* Sign into your [Apple Developer Account](https://developer.apple.com/account/)
* Go to Certificates, Identifiers and Profiles
* Register a new Pass Type Identifier under the Identifiers tab
* Create a new Pass Type ID Certificate under the Certificates tab
* Select your previously created Pass Type Identifier in the process
* Move your new certificate to the My Certificates tab in the keychain
* Export your certificate as a .p12 file

* Install node.js and download the [passkit-keys](https://github.com/walletpass/pass-js/blob/master/bin/passkit-keys) script
* Create a `keys` folder and put the .p12 file inside
* Run ./passkit-keys `<path to your keys folder>`
* You may have to type in the passphrase you defined during the export step
* Base64 encode the contents of the newly generated .pem file inside the keys folder
* Acuerdate de limpiar el archivo


# Explanation of the process

Todo el proceso de generación del archivo de pases ocurre localmente en su navegador. Para el paso de la firma, sólo se envía al servidor una representación con hash de sus datos.

En primer lugar, los siguientes pasos ocurren localmente en su navegador:

* Reconocer y extraer los datos del código QR de su certificado seleccionado.
* Descodificación de sus datos personales y sanitarios a partir de la carga útil del código QR
* Ensamblaje de un archivo de paso incompleto a partir de sus datos
* Generar un archivo que contenga los hashes de los datos almacenados en el archivo de pases
* Enviar al servidor sólo el archivo que contiene los hash.

En segundo lugar, los siguientes pasos ocurren en el servidor:

* Recibir y comprobar los hashes generados localmente.
* Firma del archivo que contiene los hashes
* Envío de la firma al servidor

Finalmente, los siguientes pasos ocurren localmente en su navegador:

* Ensamblar el archivo de paso firmado a partir del archivo incompleto generado localmente y la firma.
* Guardar el archivo en su dispositivo


# Privacy policy of our service

You can find the full privacy policy of our service [here](https://covidpass.marvinsextro.de/privacy).

# Credits

The idea for this web app originated from the [solution of an Austrian web developer](https://coronapass.fabianpimminger.com), which only works for Austrian certificates at the moment.

# Contribute

Any contribution to this project is welcome. Feel free to leave your suggestions, issues or pull requests. We are also looking for people to translate this web app for all EU countries.
