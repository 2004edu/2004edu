traductor 
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Traductor de Palabras</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.5.1/jquery.min.js"></script>
    <script>
        const apiKey = 'TU_CLAVE_DE_SUSCRIPCIÓN_AZURE'; // Reemplaza con tu clave de suscripción

        function traducir() {
            const palabra = document.getElementById("inputPalabra").value;
            const idiomaOrigen = 'es'; // Idioma de origen (español en este caso)
            const idiomaDestino = 'en'; // Idioma al que se traducirá (inglés en este caso)

            $.ajax({
                url: `https://api.cognitive.microsofttranslator.com/translate?api-version=3.0&from=${idiomaOrigen}&to=${idiomaDestino}`,
                type: 'POST',
                contentType: 'application/json',
                headers: {
                    'Ocp-Apim-Subscription-Key': apiKey,
                    'Ocp-Apim-Subscription-Region': 'westus', // Reemplaza con tu región
                },
                data: JSON.stringify([{ 'text': palabra }]),
                success: function (data) {
                    const palabraTraducida = data[0].translations[0].text;
                    document.getElementById("resultado").innerHTML = `Palabra traducida: ${palabraTraducida}`;
                },
                error: function (error) {
                    console.error('Error al traducir:', error);
                }
            });
        }
    </script>
</head>
<body>
    <h1>Traductor de Palabras</h1>
    <label for="inputPalabra">Ingresa una palabra:</label>
    <input type="text" id="inputPalabra">
    <button onclick="traducir()">Traducir</button>
    <p id="resultado"></p>
</body>
</html>

