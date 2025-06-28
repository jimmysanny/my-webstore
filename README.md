# my-webstore
modern  and stylish furniture
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Your Online Store</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap');
        
        body {
            font-family: 'Poppins', sans-serif;
            background-color: #f8f9fa;
        }

        .product-card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.1);
        }

        .btn-primary {
            background-color: #4a90e2;
            color: white;
        }

        .btn-primary:hover {
            background-color: #357abd;
        }

        #cart-sidebar, #admin-panel {
            transition: transform 0.3s ease-in-out;
        }
    </style>
</head>
<body class="text-gray-800">

    <!-- Header -->
    <header class="bg-white shadow-md sticky top-0 z-40">
        <nav class="container mx-auto px-6 py-4 flex justify-between items-center">
            <a href="#" class="text-2xl font-bold text-gray-800">MyStore</a>
            <div>
                <button id="open-admin-panel" class="mr-4 px-3 py-2 rounded-md text-sm font-medium text-gray-700 hover:bg-gray-200">
                    <i class="fas fa-user-shield mr-1"></i> Admin
                </button>
                <button id="open-cart-btn" class="relative">
                    <i class="fas fa-shopping-cart text-2xl text-gray-600"></i>
                    <span id="cart-item-count" class="absolute -top-2 -right-3 bg-red-500 text-white text-xs font-bold rounded-full h-5 w-5 flex items-center justify-center">0</span>
                </button>
            </div>
        </nav>
    </header>

    <!-- Main Content -->
    <main class="container mx-auto px-6 py-12">
        <!-- Hero Section -->
        <section class="text-center mb-16">
            <h1 class="text-4xl md:text-5xl font-bold mb-4">Welcome to Your New Store</h1>
            <p class="text-lg text-gray-600 max-w-2xl mx-auto">Discover amazing products, curated just for you. Add your own products using the admin panel!</p>
        </section>

        <!-- Product Grid -->
        <section id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-8">
            <!-- Products will be dynamically inserted here -->
        </section>
    </main>

    <!-- Footer -->
    <footer class="bg-white mt-16 py-8 border-t">
        <div class="container mx-auto px-6 text-center text-gray-600">
            <p>&copy; 2025 MyStore. All Rights Reserved.</p>
        </div>
    </footer>

    <!-- Cart Sidebar -->
    <div id="cart-sidebar" class="fixed top-0 right-0 h-full w-full sm:w-96 bg-white shadow-2xl transform translate-x-full z-50">
        <div class="flex flex-col h-full">
            <div class="p-6 border-b flex justify-between items-center">
                <h2 class="text-2xl font-bold">Your Cart</h2>
                <button id="close-cart-btn" class="text-gray-600 hover:text-gray-900">
                    <i class="fas fa-times text-2xl"></i>
                </button>
            </div>
            <div id="cart-items" class="flex-grow p-6 overflow-y-auto">
                <!-- Cart items will be dynamically inserted here -->
                <p id="empty-cart-msg" class="text-gray-500">Your cart is empty.</p>
            </div>
            <div class="p-6 border-t bg-gray-50">
                <div class="flex justify-between items-center mb-4">
                    <span class="text-lg font-semibold">Subtotal</span>
                    <span id="cart-subtotal" class="text-lg font-bold">$0.00</span>
                </div>
                <button class="w-full py-3 rounded-lg btn-primary font-bold">Proceed to Checkout</button>
            </div>
        </div>
    </div>
    
    <!-- Admin Panel -->
    <div id="admin-panel" class="fixed top-0 left-0 h-full w-full sm:w-96 bg-white shadow-2xl transform -translate-x-full z-50">
        <div class="flex flex-col h-full">
            <div class="p-6 border-b flex justify-between items-center">
                <h2 class="text-2xl font-bold">Admin Panel</h2>
                <button id="close-admin-panel" class="text-gray-600 hover:text-gray-900">
                    <i class="fas fa-times text-2xl"></i>
                </button>
            </div>
            <div class="p-6 overflow-y-auto">
                <h3 class="text-xl font-semibold mb-4">Add a New Product</h3>
                <form id="add-product-form" class="space-y-4">
                    <div>
                        <label for="product-name" class="block text-sm font-medium text-gray-700">Product Name</label>
                        <input type="text" id="product-name" required class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500">
                    </div>
                    <div>
                        <label for="product-price" class="block text-sm font-medium text-gray-700">Price ($)</label>
                        <input type="number" id="product-price" step="0.01" min="0" required class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500">
                    </div>
                    <div>
                        <label for="product-image" class="block text-sm font-medium text-gray-700">Image URL</label>
                        <input type="url" id="product-image" required class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm focus:outline-none focus:ring-blue-500 focus:border-blue-500" placeholder="https://example.com/image.jpg">
                    </div>
                    <button type="submit" class="w-full py-3 rounded-lg btn-primary font-bold">Add Product</button>
                </form>
            </div>
        </div>
    </div>
    
    <!-- Overlay -->
    <div id="overlay" class="fixed inset-0 bg-black bg-opacity-50 z-40 hidden"></div>


    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // State
            let products = [
                { id: 1, name: 'Stylish Modern Chair', price: 180.00, image: 'https://placehold.co/400x400/a3b18a/344e41?text=Chair' },
                { id: 2, name: 'Minimalist Lamp', price: 75.50, image: 'https://placehold.co/400x400/dad7cd/344e41?text=Lamp' },
                { id: 3, name: 'Oak Wood Desk', price: 320.00, image: 'https://placehold.co/400x400/588157/ffffff?text=Desk' },
                { id: 4, name: 'Cozy Throw Blanket', price: 45.00, image: 'https://placehold.co/400x400/3a5a40/ffffff?text=Blanket' }
            ];
            let cart = [];

            // Selectors
            const productGrid = document.getElementById('product-grid');
            const cartSidebar = document.getElementById('cart-sidebar');
            const adminPanel = document.getElementById('admin-panel');
            const overlay = document.getElementById('overlay');
            const openCartBtn = document.getElementById('open-cart-btn');
            const closeCartBtn = document.getElementById('close-cart-btn');
            const openAdminBtn = document.getElementById('open-admin-panel');
            const closeAdminBtn = document.getElementById('close-admin-panel');
            const cartItemsContainer = document.getElementById('cart-items');
            const cartItemCount = document.getElementById('cart-item-count');
            const emptyCartMsg = document.getElementById('empty-cart-msg');
            const cartSubtotal = document.getElementById('cart-subtotal');
            const addProductForm = document.getElementById('add-product-form');

            // --- Render Functions ---
            const renderProducts = () => {
                productGrid.innerHTML = '';
                products.forEach(product => {
                    const productEl = document.createElement('div');
                    productEl.className = 'product-card bg-white rounded-lg shadow-lg overflow-hidden flex flex-col';
                    productEl.innerHTML = `
                        <img src="${product.image}" alt="${product.name}" class="w-full h-64 object-cover" onerror="this.onerror=null;this.src='https://placehold.co/400x400/cccccc/333333?text=Image+Not+Found';">
                        <div class="p-6 flex flex-col flex-grow">
                            <h3 class="text-xl font-semibold mb-2 flex-grow">${product.name}</h3>
                            <p class="text-2xl font-bold text-gray-900 mb-4">$${product.price.toFixed(2)}</p>
                            <button class="w-full py-2 rounded-lg btn-primary mt-auto add-to-cart-btn" data-id="${product.id}">Add to Cart</button>
                        </div>
                    `;
                    productGrid.appendChild(productEl);
                });
            };

            const renderCart = () => {
                cartItemsContainer.innerHTML = '';
                if (cart.length === 0) {
                    cartItemsContainer.appendChild(emptyCartMsg);
                    emptyCartMsg.style.display = 'block';
                } else {
                    emptyCartMsg.style.display = 'none';
                    cart.forEach(item => {
                        const cartItemEl = document.createElement('div');
                        cartItemEl.className = 'flex justify-between items-center mb-4';
                        cartItemEl.innerHTML = `
                            <div class="flex items-center">
                                <img src="${item.image}" alt="${item.name}" class="w-16 h-16 object-cover rounded-md mr-4">
                                <div>
                                    <p class="font-semibold">${item.name}</p>
                                    <p class="text-gray-600">$${item.price.toFixed(2)} x ${item.quantity}</p>
                                </div>
                            </div>
                            <div class="font-bold">$${(item.price * item.quantity).toFixed(2)}</div>
                        `;
                        cartItemsContainer.appendChild(cartItemEl);
                    });
                }
                updateCartInfo();
            };

            const updateCartInfo = () => {
                const totalItems = cart.reduce((sum, item) => sum + item.quantity, 0);
                const subtotal = cart.reduce((sum, item) => sum + item.price * item.quantity, 0);
                cartItemCount.textContent = totalItems;
                cartSubtotal.textContent = `$${subtotal.toFixed(2)}`;
            };


            // --- Event Handlers ---
            const handleAddToCart = (e) => {
                if (e.target.classList.contains('add-to-cart-btn')) {
                    const productId = parseInt(e.target.dataset.id);
                    const productToAdd = products.find(p => p.id === productId);

                    const existingCartItem = cart.find(item => item.id === productId);
                    if (existingCartItem) {
                        existingCartItem.quantity++;
                    } else {
                        cart.push({ ...productToAdd, quantity: 1 });
                    }
                    renderCart();
                }
            };
            
            const handleAddProduct = (e) => {
                e.preventDefault();
                const name = document.getElementById('product-name').value;
                const price = parseFloat(document.getElementById('product-price').value);
                const image = document.getElementById('product-image').value;

                const newProduct = {
                    id: products.length > 0 ? Math.max(...products.map(p => p.id)) + 1 : 1,
                    name,
                    price,
                    image
                };

                products.push(newProduct);
                renderProducts();
                addProductForm.reset();
                alert('Product added successfully!');
                closeAdmin();
            };

            // --- UI Control Functions ---
            const openCart = () => {
                cartSidebar.classList.remove('translate-x-full');
                overlay.classList.remove('hidden');
            };
            const closeCart = () => {
                cartSidebar.classList.add('translate-x-full');
                if (adminPanel.classList.contains('-translate-x-full')) {
                    overlay.classList.add('hidden');
                }
            };

            const openAdmin = () => {
                adminPanel.classList.remove('-translate-x-full');
                overlay.classList.remove('hidden');
            };
            const closeAdmin = () => {
                adminPanel.classList.add('-translate-x-full');
                if (cartSidebar.classList.contains('translate-x-full')) {
                    overlay.classList.add('hidden');
                }
            };

            // --- Event Listeners ---
            openCartBtn.addEventListener('click', openCart);
            closeCartBtn.addEventListener('click', closeCart);
            openAdminBtn.addEventListener('click', openAdmin);
            closeAdminBtn.addEventListener('click', closeAdmin);
            overlay.addEventListener('click', () => {
                closeCart();
                closeAdmin();
            });
            productGrid.addEventListener('click', handleAddToCart);
            addProductForm.addEventListener('submit', handleAddProduct);

            // --- Initial Load ---
            renderProducts();
            renderCart();
        });
    </script>

</body>
</html>
