# Crystal-Stone-Paradise-
Online Landing Page for Crystal Stones
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Crystal Stone Paradise</title>
    <!-- Load Tailwind CSS -->
    <script src="[https://cdn.tailwindcss.com](https://cdn.tailwindcss.com)"></script>
    <link href="[https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap](https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap)" rel="stylesheet">
    <style>
        :root {
            --color-primary: #7c3aed; /* Violet-600 */
            --color-secondary: #fcd34d; /* Amber-300 */
            --color-bg: #f9fafb; /* Gray-50 */
            --color-card-bg: #ffffff;
        }
        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--color-bg);
            color: #1f2937; /* Gray-800 */
        }
        /* Custom scrollbar for better aesthetics */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: var(--color-bg); }
        ::-webkit-scrollbar-thumb { background: #d1d5db; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #9ca3af; }
    </style>
</head>
<body class="min-h-screen">
    <div id="app" class="max-w-7xl mx-auto py-8 px-4 sm:px-6 lg:px-8">

        <!-- Header: Shop name updated -->
        <header class="text-center mb-12">
            <h1 class="text-5xl font-extrabold text-gray-900 mb-2">Crystal Stone Paradise</h1>
            <p class="text-xl text-gray-600">Discover Your Inner Radiance</p>
        </header>

        <!-- Notification/Message Box -->
        <div id="message-box" class="fixed top-4 left-1/2 -translate-x-1/2 p-4 rounded-lg shadow-xl z-50 transition-all duration-300 ease-out transform scale-0" style="min-width: 300px;"></div>

        <!-- Main Shop Section -->
        <section class="mb-16">
            <h2 class="text-3xl font-semibold text-gray-800 mb-6 border-b-2 border-purple-200 pb-2">Our Featured Collection</h2>
            <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
                <!-- Products will be injected here -->
            </div>
        </section>

        <!-- Gemini Crystal Generator Section -->
        <section class="bg-violet-50 p-6 sm:p-10 rounded-xl shadow-lg border-2 border-violet-200">
            <h2 class="text-3xl font-bold text-violet-800 mb-4 flex items-center">
                <svg xmlns="[http://www.w3.org/2000/svg](http://www.w3.org/2000/svg)" class="h-8 w-8 mr-3 text-violet-600" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                    <path stroke-linecap="round" stroke-linejoin="round" d="M5 3v4M3 5h4M6 17v4m-2-2h4m5-16l2.286 6.857L21 12l-5.714 2.143L13 21l-2.286-6.857L5 12l5.714-2.143L13 3z" />
                </svg>
                Gemini Crystal Generator
            </h2>
            <p class="text-violet-600 mb-6">Describe your ultimate, unique crystal creation and see it brought to life by AI!</p>

            <div class="space-y-4">
                <input type="text" id="crystal-prompt" class="w-full p-3 border border-violet-300 rounded-lg focus:ring-violet-500 focus:border-violet-500 transition duration-150" placeholder="A shimmering phantom quartz cluster, glowing cyan and gold...">
                <button id="generate-button" class="w-full sm:w-auto px-6 py-3 bg-violet-600 text-white font-semibold rounded-lg shadow-md hover:bg-violet-700 transition duration-150 transform hover:scale-[1.01] active:scale-[0.99] disabled:opacity-50">
                    Generate Unique Crystal Image
                </button>
            </div>

            <div id="generator-result" class="mt-8 p-4 bg-white rounded-lg shadow-inner flex flex-col items-center">
                <p id="initial-message" class="text-gray-500 text-center">Your generated image will appear here.</p>
                <div id="loading-indicator" class="hidden text-center">
                    <div class="animate-spin rounded-full h-10 w-10 border-b-2 border-violet-500 mb-3 mx-auto"></div>
                    <p class="text-violet-600 font-medium">Manifesting your crystal...</p>
                </div>
                <img id="generated-image" class="hidden w-full max-w-sm rounded-lg shadow-xl border-4 border-white" src="" alt="Generated Crystal">
                <button id="custom-purchase-button" class="hidden mt-4 px-4 py-2 bg-amber-500 text-gray-800 font-bold rounded-lg shadow-md hover:bg-amber-600 transition duration-150 transform hover:scale-[1.05] active:scale-[0.95]">
                    Simulate Purchase of Custom Crystal (R99.99)
                </button>
            </div>
        </section>

        <!-- Product Modal (Hidden by default) -->
        <div id="product-modal" class="hidden fixed inset-0 bg-gray-900 bg-opacity-75 z-50 flex items-center justify-center p-4">
            <div class="bg-white rounded-xl shadow-2xl max-w-lg w-full p-6 relative">
                <button onclick="closeModal()" class="absolute top-3 right-3 text-gray-500 hover:text-gray-900 transition duration-150">
                    <svg xmlns="[http://www.w3.org/2000/svg](http://www.w3.org/2000/svg)" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" /></svg>
                </button>
                <img id="modal-image" class="w-full h-48 object-cover rounded-lg mb-4 shadow-md" src="" alt="Product Image">
                <h3 id="modal-name" class="text-3xl font-bold text-gray-900 mb-2"></h3>
                <p id="modal-description" class="text-gray-600 mb-4"></p>
                <p id="modal-price" class="text-2xl font-extrabold text-violet-600 mb-6"></p>
                <button onclick="simulatePurchaseFromModal()" class="w-full px-4 py-3 bg-violet-600 text-white font-semibold rounded-lg shadow-md hover:bg-violet-700 transition duration-150 transform hover:scale-[1.01] active:scale-[0.99]">
                    Add to Cart
                </button>
            </div>
        </div>

    </div>

    <script type="module">
        // Global variables for Firebase context (required for compilation environment)
        // These are intentionally empty or default as Firebase is not used for this static app.
        const __app_id = 'default-crystal-app';
        const __firebase_config = '{}';
        const __initial_auth_token = '';
        const appId = typeof __app_id !== 'undefined' ? __app_id : 'default-app-id';

        // --- Core Application Data ---
        // Prices are listed in Rands (R)
        const crystals = [
            { id: 1, name: "Amethyst Cluster", price: 29.99, description: "Known for promoting **calm, balance, and peace**. This stunning deep purple cluster is perfect for meditation, stress relief, and fostering spiritual awareness.", color: "bg-purple-600", image: "[https://placehold.co/400x300/8B5CF6/ffffff?text=Amethyst+Cluster](https://placehold.co/400x300/8B5CF6/ffffff?text=Amethyst+Cluster)" },
            { id: 2, name: "Rose Quartz Heart", price: 15.50, description: "The stone of **universal love**. It restores trust and harmony in relationships, encouraging unconditional love, deep inner healing, and feelings of peace.", color: "bg-pink-400", image: "[https://placehold.co/400x300/F472B6/374151?text=Rose+Quartz+Heart](https://placehold.co/400x300/F472B6/374151?text=Rose+Quartz+Heart)" },
            { id: 3, name: "Citrine Tower", price: 45.00, description: "A joyous stone that carries the power of the sun. **Attracts wealth, success, and prosperity**. It promotes motivation, activates creativity, and encourages self-expression.", color: "bg-yellow-500", image: "[https://placehold.co/400x300/FCD34D/374151?text=Citrine+Tower](https://placehold.co/400x300/FCD34D/374151?text=Citrine+Tower)" },
            { id: 4, name: "Black Tourmaline", price: 19.99, description: "A powerful stone for **protection and grounding**. It shields against negative energies and electromagnetic smog, providing a deep sense of security and vitality.", color: "bg-gray-800", image: "[https://placehold.co/400x300/1f2937/ffffff?text=Black+Tourmaline](https://placehold.co/400x300/1f2937/ffffff?text=Black+Tourmaline)" },
            { id: 5, name: "Clear Quartz Point", price: 35.75, description: "The **master healer and energy amplifier**. It absorbs, stores, releases, and regulates energy, and is excellent for intention setting and cleansing other stones.", color: "bg-gray-200", image: "[https://placehold.co/400x300/e5e7eb/374151?text=Clear+Quartz+Point](https://placehold.co/400x300/e5e7eb/374151?text=Clear+Quartz+Point)" },
            { id: 6, name: "Labradorite Palm", price: 22.99, description: "Known as the **stone of magic**. It awakens inner awareness, strengthens intuition, and offers protection against negative psychic energies during transition.", color: "bg-blue-600", image: "[https://placehold.co/400x300/2563EB/ffffff?text=Labradorite+Palm](https://placehold.co/400x300/2563EB/ffffff?text=Labradorite+Palm)" },

            // Additional Popular Crystals
            { id: 7, name: "Green Aventurine", price: 18.99, description: "A stone of **prosperity and confidence**. It promotes compassion, encourages perseverance, and stabilizes the mind, making it a powerful good luck charm and comforter.", color: "bg-green-400", image: "[https://placehold.co/400x300/4ADE80/166534?text=Green+Aventurine](https://placehold.co/400x300/4ADE80/166534?text=Green+Aventurine)" },
            { id: 8, name: "Lapis Lazuli Tumble", price: 12.00, description: "The stone of **wisdom and truth**. It rapidly releases stress, bringing deep peace. It encourages self-awareness, honesty, and clear communication in your life.", color: "bg-blue-800", image: "[https://placehold.co/400x300/1E40AF/ffffff?text=Lapis+Lazuli](https://placehold.co/400x300/1E40AF/ffffff?text=Lapis+Lazuli)" },
            { id: 9, name: "Tiger's Eye Orb", price: 25.49, description: "A crystal of **protection and good fortune**. It focuses the mind, dispels fear, and promotes clarity of intention, boosting courage and self-integrity in difficult situations.", color: "bg-yellow-700", image: "[https://placehold.co/400x300/B45309/FCD34D?text=Tiger's+Eye](https://placehold.co/400x300/B45309/FCD34D?text=Tiger's+Eye)" },
            { id: 10, name: "Selenite Wand", price: 10.99, description: "Known for **cleansing and purification**. It provides peace, clarity, and access to angelic consciousness. Selenite is essential for charging and clearing other crystals.", color: "bg-gray-100", image: "[https://placehold.co/400x300/F3F4F6/374151?text=Selenite+Wand](https://placehold.co/400x300/F3F4F6/374151?text=Selenite+Wand)" },
            { id: 11, name: "Carnelian Pebble", price: 9.50, description: "The stone of **vitality and motivation**. It restores lost energy, stimulates creativity, and encourages boldness. Perfect for igniting your inner fire and promoting positive life choices.", color: "bg-red-600", image: "[https://placehold.co/400x300/DC2626/FED7AA?text=Carnelian+Pebble](https://placehold.co/400x300/DC2626/FED7AA?text=Carnelian+Pebble)" },
            { id: 12, name: "Red Garnet Nugget", price: 39.99, description: "A stone of **passion and commitment**. It revitalizes feelings, inspires love, and fortifies courage. It is often used for grounding, protection, and to stimulate the metabolism.", color: "bg-red-800", image: "[https://placehold.co/400x300/991B1B/FCA5A5?text=Red+Garnet](https://placehold.co/400x300/991B1B/FCA5A5?text=Red+Garnet)" },
            { id: 13, name: "Sodalite Pyramid", price: 28.00, description: "Promotes **logic, rationality, and emotional balance**. It encourages self-acceptance and self-trust, helping to calm panic attacks and ease phobias and fear.", color: "bg-blue-900", image: "[https://placehold.co/400x300/1D4ED8/DBEAFE?text=Sodalite+Pyramid](https://placehold.co/400x300/1D4ED8/DBEAFE?text=Sodalite+Pyramid)" },
            { id: 14, name: "Hematite Magnet", price: 16.50, description: "Highly effective for **grounding and balancing**. It dissolves negativity and prevents you from absorbing the negativity of others, strengthening willpower and reliability.", color: "bg-gray-700", image: "[https://placehold.co/400x300/4B5563/F9FAFB?text=Hematite](https://placehold.co/400x300/4B5563/F9FAFB?text=Hematite)" },
            { id: 15, name: "Malachite Sphere", price: 55.00, description: "A stone of **transformation and emotional release**. It clears and activates the chakras, stimulating deep emotional healing and protecting against negative influences.", color: "bg-green-700", image: "[https://placehold.co/400x300/065F46/D1FAE5?text=Malachite+Sphere](https://placehold.co/400x300/065F46/D1FAE5?text=Malachite+Sphere)" },
            { id: 16, name: "Rainbow Moonstone", price: 32.99, description: "The stone of **new beginnings and intuition**. It soothes emotional instability and stress, providing calmness, and enhancing psychic abilities and prophetic dreams.", color: "bg-white", image: "[https://placehold.co/400x300/FFFFFF/374151?text=Moonstone](https://placehold.co/400x300/FFFFFF/374151?text=Moonstone)" },
            { id: 17, name: "Pyrite Cube", price: 21.00, description: "Also known as **'Fool's Gold'**, it's a superb energy shield. It promotes positive thinking, attracts abundance, and helps overcome fatigue and inertia.", color: "bg-yellow-600", image: "[https://placehold.co/400x300/D97706/F9FAFB?text=Pyrite+Cube](https://placehold.co/400x300/D97706/F9FAFB?text=Pyrite+Cube)" },
            { id: 18, name: "Amazonite Chunk", price: 17.50, description: "A soothing stone that **calms the brain and nervous system**. It aids in harmonious communication, balances masculine and feminine energies, and alleviates worry and fear.", color: "bg-teal-400", image: "[https://placehold.co/400x300/2DD4BF/064E3B?text=Amazonite+Chunk](https://placehold.co/400x300/2DD4BF/064E3B?text=Amazonite+Chunk)" },
            { id: 19, name: "Smoky Quartz Tumble", price: 11.99, description: "An excellent **grounding and detoxifying stone**. It gently neutralizes negative vibrations, relieving stress and tension, and promoting positive action in difficult times.", color: "bg-stone-600", image: "[https://placehold.co/400x300/57534E/FFFFFF?text=Smoky+Quartz](https://placehold.co/400x300/57534E/FFFFFF?text=Smoky+Quartz)" },
            { id: 20, name: "Rhodochrosite Slice", price: 59.99, description: "The stone of the **compassionate heart**. It gently draws out deep-seated emotional pain, encouraging a positive, cheerful outlook and attracting a soulmate.", color: "bg-pink-300", image: "[https://placehold.co/400x300/F9A8D4/831843?text=Rhodochrosite](https://placehold.co/400x300/F9A8D4/831843?text=Rhodochrosite)" },
            { id: 21, name: "Rainbow Fluorite", price: 27.50, description: "Highly protective, especially on a psychic level. It **cleanses and stabilizes the aura**, promoting concentration and rapid organization of information, making it ideal for study.", color: "bg-lime-500", image: "[https://placehold.co/400x300/84CC16/1A202C?text=Rainbow+Fluorite](https://placehold.co/400x300/84CC16/1A202C?text=Rainbow+Fluorite)" },
        ];

        // Currently selected product for modal
        let currentProduct = null;

        // --- Utility Functions ---

        /**
         * Shows a transient, custom message box instead of alert().
         * @param {string} message - The message to display.
         * @param {string} type - 'success', 'error', or 'info'.
         */
        function showMessage(message, type = 'info') {
            const box = document.getElementById('message-box');
            box.textContent = message;

            let bgColor = 'bg-blue-500';
            let textColor = 'text-white';

            if (type === 'success') {
                bgColor = 'bg-green-500';
            } else if (type === 'error') {
                bgColor = 'bg-red-500';
            }

            box.className = `fixed top-4 left-1/2 -translate-x-1/2 p-4 rounded-lg shadow-xl z-50 transition-all duration-300 ease-out transform ${bgColor} ${textColor}`;
            box.style.transform = 'translate(-50%, 0) scale(1)';

            setTimeout(() => {
                box.style.transform = 'translate(-50%, 0) scale(0)';
            }, 3000);
        }

        // --- Shop Logic ---

        /**
         * Renders the product cards into the grid.
         */
        function renderProducts() {
            const grid = document.getElementById('product-grid');
            grid.innerHTML = ''; // Clear existing content

            crystals.forEach(crystal => {
                // Determine base color class for the placeholder background/border
                const baseColor = crystal.color;
                
                const card = document.createElement('div');
                card.className = "bg-white rounded-xl shadow-lg hover:shadow-xl transition-shadow duration-300 overflow-hidden cursor-pointer transform hover:scale-[1.02] active:scale-[1.01]";
                card.innerHTML = `
                    <img src="${crystal.image}" alt="${crystal.name}" class="w-full h-48 object-cover ${baseColor} border-b-4 border-violet-100" onerror="this.onerror=null; this.src='[https://placehold.co/400x300/D1D5DB/1F2937?text=Crystal](https://placehold.co/400x300/D1D5DB/1F2937?text=Crystal)';">
                    <div class="p-5">
                        <h3 class="text-xl font-bold text-gray-900 mb-1">${crystal.name}</h3>
                        <p class="text-lg font-semibold text-violet-600 mb-3">R${crystal.price.toFixed(2)}</p>
                        <button data-id="${crystal.id}" class="view-product-btn w-full px-3 py-2 text-sm bg-violet-100 text-violet-700 font-medium rounded-lg hover:bg-violet-200 transition">View Details</button>
                    </div>
                `;
                grid.appendChild(card);
            });

            // Attach event listeners for viewing details
            document.querySelectorAll('.view-product-btn').forEach(button => {
                button.addEventListener('click', (e) => {
                    const id = parseInt(e.target.dataset.id);
                    openModal(id);
                });
            });
        }

        /**
         * Opens the product detail modal.
         * @param {number} id - The ID of the crystal to display.
         */
        window.openModal = function(id) {
            currentProduct = crystals.find(c => c.id === id);
            if (!currentProduct) return;

            document.getElementById('modal-image').src = currentProduct.image;
            document.getElementById('modal-image').alt = currentProduct.name;
            document.getElementById('modal-name').textContent = currentProduct.name;
            // Use innerHTML to allow bold tags from the description to render
            document.getElementById('modal-description').innerHTML = currentProduct.description; 
            document.getElementById('modal-price').textContent = `R${currentProduct.price.toFixed(2)}`;

            document.getElementById('product-modal').classList.remove('hidden');
        }

        /**
         * Closes the product detail modal.
         */
        window.closeModal = function() {
            document.getElementById('product-modal').classList.add('hidden');
            currentProduct = null;
        }

        /**
         * Simulates adding the current product to the cart and notifies the user.
         */
        window.simulatePurchaseFromModal = function() {
            if (currentProduct) {
                showMessage(`Successfully added ${currentProduct.name} to your cart! Price: R${currentProduct.price.toFixed(2)}`, 'success');
                closeModal();
            }
        }

        // --- Image Generation Logic ---

        const generateButton = document.getElementById('generate-button');
        const crystalPromptInput = document.getElementById('crystal-prompt');
        const loadingIndicator = document.getElementById('loading-indicator');
        const generatedImage = document.getElementById('generated-image');
        const customPurchaseButton = document.getElementById('custom-purchase-button');
        const initialMessage = document.getElementById('initial-message');

        let isLoading = false;

        const apiKey = "";
        const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/imagen-3.0-generate-002:predict?key=${apiKey}`;

        /**
         * Generates a crystal image using the Imagen API.
         */
        async function generateCrystalImage() {
            if (isLoading) return;

            const prompt = crystalPromptInput.value.trim();
            if (!prompt) {
                showMessage("Please enter a description for your custom crystal.", 'info');
                return;
            }

            // Set loading state
            isLoading = true;
            generateButton.disabled = true;
            loadingIndicator.classList.remove('hidden');
            initialMessage.classList.add('hidden');
            generatedImage.classList.add('hidden');
            customPurchaseButton.classList.add('hidden');

            const fullPrompt = `Photorealistic image of a high-quality, shimmering crystal, centered, elegant studio lighting, detailed macro shot, natural mineral texture. The crystal is described as: "${prompt}"`;

            // Function to handle exponential backoff for retries
            const MAX_RETRIES = 3;
            for (let i = 0; i < MAX_RETRIES; i++) {
                try {
                    const payload = {
                        instances: { prompt: fullPrompt },
                        parameters: {
                            sampleCount: 1,
                            outputMimeType: "image/png",
                            aspectRatio: "1:1"
                        }
                    };

                    const response = await fetch(apiUrl, {
                        method: 'POST',
                        headers: { 'Content-Type': 'application/json' },
                        body: JSON.stringify(payload)
                    });

                    if (response.status === 429 && i < MAX_RETRIES - 1) {
                        // Rate limit error, wait and retry
                        const delay = Math.pow(2, i) * 1000;
                        await new Promise(resolve => setTimeout(resolve, delay));
                        continue; 
                    }
                    
                    if (!response.ok) {
                        throw new Error(`API error: ${response.status} ${response.statusText}`);
                    }

                    const result = await response.json();

                    if (result.predictions && result.predictions.length > 0 && result.predictions[0].bytesBase64Encoded) {
                        const base64Data = result.predictions[0].bytesBase64Encoded;
                        const imageUrl = `data:image/png;base64,${base64Data}`;

                        generatedImage.src = imageUrl;
                        generatedImage.alt = `Generated Crystal: ${prompt}`;
                        generatedImage.classList.remove('hidden');
                        customPurchaseButton.classList.remove('hidden');
                        showMessage("Your custom crystal has manifested!", 'success');
                        return; // Exit function on success

                    } else {
                        showMessage("Failed to generate crystal image. Please try a different prompt.", 'error');
                        generatedImage.classList.add('hidden');
                        return; // Exit function on failure
                    }

                } catch (error) {
                    console.error("Error generating image:", error);
                    if (i === MAX_RETRIES - 1) {
                        showMessage("An error occurred during generation after multiple retries. Check the console for details.", 'error');
                    } else {
                        const delay = Math.pow(2, i) * 1000;
                        await new Promise(resolve => setTimeout(resolve, delay));
                    }
                }
            } // End of retry loop

            // Reset loading state if the loop finishes without success
            isLoading = false;
            generateButton.disabled = false;
            loadingIndicator.classList.add('hidden');
            initialMessage.classList.remove('hidden');
        }

        /**
         * Simulates purchase of the generated custom item.
         */
        window.simulateCustomPurchase = function() {
            const prompt = crystalPromptInput.value.trim() || 'Unique Custom Crystal';
            // Currency and price updated here
            showMessage(`Simulating purchase of the custom crystal: "${prompt}" for R99.99. Enjoy your bespoke gem!`, 'success');
            // Clear the generator for the next creation
            generatedImage.classList.add('hidden');
            customPurchaseButton.classList.add('hidden');
            initialMessage.classList.remove('hidden');
            crystalPromptInput.value = '';
        }

        // --- Initialization ---
        document.addEventListener('DOMContentLoaded', () => {
            renderProducts();

            // Attach listeners for generator
            generateButton.addEventListener('click', generateCrystalImage);
            customPurchaseButton.addEventListener('click', window.simulateCustomPurchase);
        });

    </script>
</body>
</html>

