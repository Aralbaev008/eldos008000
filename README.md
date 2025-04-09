<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Аренда автомобилей – ZhaponCar</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #1a1a1a; color: #fff; }
        header { background: #000; color: #ffcc00; text-align: center; padding: 15px; font-size: 28px; font-weight: bold; display: flex; align-items: center; justify-content: center; gap: 15px; }
        .logo { width: 60px; height: 60px; border-radius: 50%; }
        .container { max-width: 1200px; margin: auto; padding: 20px; display: flex; flex-wrap: wrap; justify-content: space-around; }
        .car { background: #333; padding: 15px; margin: 15px; border-radius: 10px; width: 30%; text-align: center; box-shadow: 0 0 10px rgba(255, 204, 0, 0.7); transition: 0.3s; }
        .car img { width: 100%; max-height: 200px; object-fit: cover; border-radius: 5px; }
        .price { font-size: 22px; color: #ffcc00; margin: 10px 0; font-weight: bold; }
        .btn { padding: 10px 20px; background: #ffcc00; color: #000; border: none; cursor: pointer; font-weight: bold; border-radius: 5px; margin-top: 10px; }
        .btn:hover { background: #e6b800; }
        .cart { background: #222; padding: 20px; border-radius: 10px; margin: 20px auto; max-width: 600px; box-shadow: 0 0 10px rgba(255, 204, 0, 0.7); text-align: center; }
        .cart ul { list-style: none; padding: 0; }
        .cart li { margin: 10px 0; padding: 10px; background: #333; border-radius: 5px; }
        .remove-btn { background: red; color: white; padding: 5px 10px; border: none; cursor: pointer; border-radius: 5px; }
        footer { background: #000; color: #ffcc00; text-align: center; padding: 10px; margin-top: 20px; font-weight: bold; }
        @media (max-width: 768px) { .car { width: 90%; } }
    </style>
</head>
<body>

<header>
    🚗 Аренда автомобилей – ZhaponCar
</header>

<div class="container" id="cars"></div>

<section class="cart">
    <h2>🛒 Корзина</h2>
    <ul id="cart-list"></ul>
    <p id="cart-total">Итого: 0₸</p>
</section>

<footer>
    📞 Контакты: +7 777 931 1717 | ✉️ Email: ZhaponCar.com
</footer>

<script>
    let cars = [
        { name: "Hyundai Accent", price: 30000, img: "accent.jpg" },
        { name: "Toyota Camry", price: 60000, img: "camry.jpg" },
        { name: "BMW 5-Series", price: 150000, img: "bmw5.jpg" },
        { name: "Mercedes E-Class", price: 90000, img: "eclass.jpg" },
        { name: "Audi A6", price: 22000, img: "a6.jpg" },
        { name: "Lexus RX", price: 50000, img: "lexus.jpg" },
        { name: "Porsche Panamera", price: 100000, img: "panamera.jpg" },
        { name: "Mercedes G-Class", price: 200000, img: "gclass.jpg" }
    ];

    let cart = [];

    function loadCars() {
        let carsContainer = document.getElementById("cars");
        cars.forEach(car => {
            let carDiv = document.createElement("div");
            carDiv.classList.add("car");
            carDiv.innerHTML = `
                <img src="${car.img}" alt="${car.name}">
                <h3>${car.name}</h3>
                <div class="price">Цена: ${car.price}₸/день</div>
                <button class="btn" onclick="addToCart('${car.name}', ${car.price})">Добавить в корзину</button>
            `;
            carsContainer.appendChild(carDiv);
        });
    }

    function addToCart(name, price) {
        cart.push({ name, price });
        updateCart();
    }

    function removeFromCart(index) {
        cart.splice(index, 1);
        updateCart();
    }

    function updateCart() {
        const cartList = document.getElementById("cart-list");
        const cartTotal = document.getElementById("cart-total");
        cartList.innerHTML = "";
        let total = 0;

        cart.forEach((item, index) => {
            total += item.price;
            cartList.innerHTML += `
                <li>
                    ${item.name} - ${item.price}₸ 
                    <button class="remove-btn" onclick="removeFromCart(${index})">Удалить</button>
                </li>
            `;
        });

        cartTotal.innerHTML = `Итого: ${total}₸`; // Исправлено здесь
    }

    loadCars(); // Загружаем все автомобили при старте страницы
</script>

</body>
</html>
