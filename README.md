        // Datos del juego: Preguntas, opciones, respuesta correcta y fondo para cada nivel
        const gameData = [
            {
                level: 1,
                question: "¿Qué debes hacer si ves el mango de una sartén caliente sobresaliendo de la estufa?",
                options: ["Tocarlo para ver si está caliente", "Avisar a un adulto para que lo mueva", "Jugar cerca de la estufa"],
                correctAnswer: "Avisar a un adulto para que lo mueva",
                backgroundImage: "https://placehold.co/700x300/FFDDC1/333333?text=Nivel+1+-+Cocina"
            },
            {
                level: 2,
                question: "¿Es seguro meter los dedos u objetos en los enchufes eléctricos?",
                options: ["Sí, si lo hago rápido", "No, es muy peligroso", "Solo si mis manos están secas"],
                correctAnswer: "No, es muy peligroso",
                backgroundImage: "https://placehold.co/700x300/C1E1FF/333333?text=Nivel+2+-+Enchufes"
            },
            {
                level: 3,
                question: "¿Qué debes hacer si alguien va a pasar cerca de ti con una taza de líquido caliente?",
                options: ["Quedarme quieto y dejar que pase", "Correr y jugar a su alrededor", "Intentar agarrar la taza"],
                correctAnswer: "Quedarme quieto y dejar que pase",
                backgroundImage: "https://placehold.co/700x300/D1FFC1/333333?text=Nivel+3+-+Líquidos"
            },
            {
                level: 4,
                question: "Si tu ropa se prende fuego, ¿qué debes hacer?",
                options: ["Correr muy rápido para que el viento lo apague", "Detenerte, tirarte al suelo y rodar", "Gritar y esperar ayuda sin moverte"],
                correctAnswer: "Detenerte, tirarte al suelo y rodar",
                backgroundImage: "https://placehold.co/700x300/FFC1C1/333333?text=Nivel+4+-+Ropa+en+Llamas"
            },
            {
                level: 5,
                question: "Si te quemas levemente, ¿qué es lo primero que debes hacer con la quemadura?",
                options: ["Ponerle hielo directamente", "Poner la zona bajo agua fría (no helada) por varios minutos", "Aplicar pasta de dientes"],
                correctAnswer: "Poner la zona bajo agua fría (no helada) por varios minutos",
                backgroundImage: "https://placehold.co/700x300/C1FFFF/333333?text=Nivel+5+-+Primeros+Auxilios"
            },
            {
                level: 6,
                question: "¿Es seguro jugar con fósforos o encendedores?",
                options: ["Sí, si no hay adultos cerca", "No, nunca se debe jugar con fuego", "Solo si es para prender una vela de cumpleaños"],
                correctAnswer: "No, nunca se debe jugar con fuego",
                backgroundImage: "https://placehold.co/700x300/FFE0B2/333333?text=Nivel+6+-+Fósforos"
            },
            {
                level: 7,
                question: "¿Qué debes hacer si ves cables eléctricos pelados o rotos?",
                options: ["Tocarlos para ver si dan chispas", "No tocarlos y avisar a un adulto inmediatamente", "Intentar arreglarlos con cinta adhesiva"],
                correctAnswer: "No tocarlos y avisar a un adulto inmediatamente",
                backgroundImage: "https://placehold.co/700x300/E1BEE7/333333?text=Nivel+7+-+Cables"
            },
            {
                level: 8,
                question: "Al usar protector solar, ¿estás protegido de quemaduras solares todo el día con una sola aplicación?",
                options: ["Sí, una vez es suficiente", "No, hay que aplicarlo varias veces, especialmente después de nadar", "El protector solar no previene quemaduras"],
                correctAnswer: "No, hay que aplicarlo varias veces, especialmente después de nadar",
                backgroundImage: "https://placehold.co/700x300/FFF9C4/333333?text=Nivel+8+-+Sol"
            },
            {
                level: 9,
                question: "¿Qué es importante recordar sobre los hornos y estufas calientes?",
                options: ["Se pueden tocar después de usarlos porque se enfrían rápido", "Solo queman si están encendidos con llama", "Mantenerse alejado y no tocarlos, pueden estar muy calientes incluso apagados"],
                correctAnswer: "Mantenerse alejado y no tocarlos, pueden estar muy calientes incluso apagados",
                backgroundImage: "https://placehold.co/700x300/B2DFDB/333333?text=Nivel+9+-+Horno"
            },
            {
                level: 10,
                question: "¿Cuál es el número de emergencia más común al que llamar en caso de un incendio grave o accidente?",
                options: ["El de la tienda de juguetes", "911 (o el número local de tu país)", "El de un restaurante cercano"],
                correctAnswer: "911 (o el número local de tu país)",
                backgroundImage: "https://placehold.co/700x300/F8BBD0/333333?text=Nivel+10+-+Emergencia"
            }
        ];

        let currentLevelIndex = 0;

        // Función para cargar un nivel
        function loadLevel(levelIndex) {
            if (levelIndex >= gameData.length) {
                showEndGameScreen();
                return;
            }

            const levelData = gameData[levelIndex];
            levelTitle.textContent = `Nivel ${levelData.level}`;
            questionText.textContent = levelData.question;
            backgroundArea.style.backgroundImage = `url('${levelData.backgroundImage}')`;
            
            optionsContainer.innerHTML = ''; // Limpiar opciones anteriores
            messageArea.textContent = '';
            messageArea.className = 'message-area'; // Reset class
            nextButton.style.display = 'none';

            levelData.options.forEach(optionText => {
                const button = document.createElement('button');
                button.textContent = optionText;
                button.classList.add('option-button');
                button.onclick = () => handleAnswer(optionText, levelData.correctAnswer, button);
                optionsContainer.appendChild(button);
            });
        }

        // Función para manejar la respuesta del usuario
        function handleAnswer(selectedOption, correctAnswer, button) {
            // Deshabilitar todos los botones de opción después de una selección
            const optionButtons = optionsContainer.querySelectorAll('.option-button');
            optionButtons.forEach(btn => {
                btn.disabled = true;
                if (btn.textContent === correctAnswer) {
                    btn.style.backgroundColor = '#28a745'; // Verde para la correcta
                } else if (btn.textContent === selectedOption) {
                    btn.style.backgroundColor = '#dc3545'; // Rojo para la incorrecta seleccionada
                }
            });

            if (selectedOption === correctAnswer) {
                messageArea.textContent = "¡Correcto! Muy bien.";
                messageArea.className = 'message-area message-correct';
            } else {
                messageArea.textContent = `Te quemaste... ¡Cuidado! La respuesta correcta era: "${correctAnswer}"`;
                messageArea.className = 'message-area message-incorrect';
            }
            nextButton.style.display = 'block'; // Mostrar botón para continuar
        }

        // Función para el botón "Siguiente Nivel"
        nextButton.onclick = () => {
            currentLevelIndex++;
            loadLevel(currentLevelIndex);
        };

        // Función para mostrar la pantalla final del juego
        function showEndGameScreen() {
            gameContaine
