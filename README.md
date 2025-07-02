<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FoodBunny Order Confirmation</title>
    <!-- Google Font: Inter -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom styles for the Inter font */
        body {
            font-family: 'Inter', sans-serif;
            background-color: #FFF3E0; /* Very light orange/cream background to match FoodBunny theme */
            display: flex;
            flex-direction: column; /* Stack card vertically */
            justify-content: center;
            align-items: center;
            min-height: 100vh; /* Ensure it takes full viewport height */
            padding: 1rem; /* Add some padding for smaller screens */
            box-sizing: border-box; /* Include padding in element's total width and height */
        }
        /* Ensure the button text is readable */
        .copy-button:active {
            background-color: #E65100; /* Darker orange on active */
        }
    </style>
</head>
<body>
    <!-- The FoodBunny Logo div has been removed as per your request -->

    <div class="w-full max-w-md mx-auto bg-white p-6 md:p-8 rounded-xl shadow-lg border border-orange-200">
        <!-- Order Details Card -->
        <div id="order-details-card" class="text-gray-800">
            <h1 class="text-3xl md:text-4xl font-bold text-center mb-6 text-pink-600" contenteditable="true">FoodBunny</h1>
            <p class="text-lg md:text-xl font-semibold mb-4 text-orange-700" contenteditable="true">Your Order Details:</p>
            <p class="text-base md:text-lg mb-2" contenteditable="true">Your Name: <span id="customer-name" class="font-medium">John Doe</span></p>
            <p class="text-base md:text-lg mb-2" contenteditable="true">Your Address: <span id="customer-address" class="font-medium">123 Main St, Anytown, USA</span></p>
            <p class="text-base md:text-lg mb-6" contenteditable="true">Your Number: <span id="customer-number" class="font-medium">+1234567890</span></p>
            <p class="text-lg md:text-xl font-semibold text-center text-pink-700" contenteditable="true">Apna Order confirm kare 'Ok' likh kar.</p>
        </div>

        <!-- Copy Button -->
        <div class="mt-8 text-center">
            <button id="copyButton" class="copy-button bg-orange-500 hover:bg-orange-600 text-white font-semibold py-3 px-6 rounded-lg shadow-md transition duration-300 ease-in-out focus:outline-none focus:ring-2 focus:ring-orange-500 focus:ring-opacity-75">
                Copy Order
            </button>
            <p id="copyFeedback" class="text-sm text-gray-600 mt-2 opacity-0 transition-opacity duration-300"></p>
        </div>
    </div>

    <script>
        // Get the copy button and feedback element
        const copyButton = document.getElementById('copyButton');
        const copyFeedback = document.getElementById('copyFeedback');
        const orderDetailsCard = document.getElementById('order-details-card');

        // Add a click event listener to the copy button
        copyButton.addEventListener('click', function() {
            // Get all the text content from the order details card
            // We use innerText to get the visible text, ignoring HTML tags
            const textToCopy = orderDetailsCard.innerText;

            // Create a temporary textarea element to hold the text
            const tempTextArea = document.createElement('textarea');
            tempTextArea.value = textToCopy;
            document.body.appendChild(tempTextArea);

            // Select the text in the textarea
            tempTextArea.select();
            tempTextArea.setSelectionRange(0, 99999); /* For mobile devices */

            try {
                // Execute the copy command
                document.execCommand('copy');
                // Provide user feedback
                copyFeedback.textContent = 'Copied to clipboard!';
                copyFeedback.classList.remove('opacity-0');
                copyFeedback.classList.add('opacity-100');

                // Temporarily change button text for visual feedback
                const originalButtonText = copyButton.textContent;
                copyButton.textContent = 'Copied!';
                setTimeout(() => {
                    copyButton.textContent = originalButtonText;
                    copyFeedback.classList.remove('opacity-100');
                    copyFeedback.classList.add('opacity-0');
                }, 2000); // Revert after 2 seconds

            } catch (err) {
                console.error('Failed to copy text: ', err);
                copyFeedback.textContent = 'Failed to copy text. Please try manually.';
                copyFeedback.classList.remove('opacity-0');
                copyFeedback.classList.add('opacity-100');
            } finally {
                // Remove the temporary textarea
                document.body.removeChild(tempTextArea);
            }
        });
    </script>
</body>
</html>
