Step 1: Create a Custom App
Run the following command in your Frappe Bench directory:

cd ../home/frappe/frappe-bench/
bench new-app dc_theme

Now install the app on your site:

bench --site site1.local install-app dc_theme


Step 2: Add Custom CSS
Navigate to the public/css directory of your new app:

cd apps/dc_theme/dc_theme/public
mkdir css
nano css/custom.css
Add the following CSS:

@font-face {
    font-family: 'Cairo Saudi';
    src: url('https://cdn.jsdelivr.net/gh/UsmanSanawar/Cairo-with-Saudi-Currency@main/Cairo-Regular-Saudi.ttf') format('truetype');
    font-weight: normal;
    font-style: normal;
}

body, .currency-symbol {
    font-family: 'Cairo Saudi', sans-serif !important;
}


Step 3: Link CSS in hooks.py
Now, open the hooks.py file in your custom app:

nano ../hooks.py

Find the app_include_css section and add:

python:
app_include_css = "/assets/dc_theme/css/custom.css"


Step 4: Build and Restart
Now, run the following commands to apply the changes:

bench build
bench restart

-----------------------------------------------
Additional Changes for Saudi Currency Symbol:
Currency Symbol to be used
xyz.com/app/currency/SAR: "§"

Add the following in print formats:

<style>	
	/* Styles for currency amounts (amounts, taxes, etc.) */
	@font-face {
		font-family: 'Cairo Saudi';
		src: url('https://cdn.jsdelivr.net/gh/UsmanSanawar/Cairo-with-Saudi-Currency@main/Cairo-Regular-Saudi.ttf') format('truetype');
	}

	.currency {
		font-family: 'Cairo Saudi', serif !important;
		direction: ltr !important;
	}

	/* Override currency styles for print */
	@media print {
		.currency {
			font-family: 'Cairo Saudi', serif !important;
			direction: ltr !important;
		}
	}
	
</style>

Use class = "currency" for Amounts, Taxes etc.


To use ttf via cdn as raw, use the link: https://cdn.jsdelivr.net/gh/UsmanSanawar/Cairo-with-Saudi-Currency@main/Cairo-Regular-Saudi.ttf

