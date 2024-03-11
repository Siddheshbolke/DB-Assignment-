1. Explain the relationship between the "Product" and "Product_Category" entities from the above diagram.
Ans:-
The relationship between the "Product" and "Product_Category" entities typically represents a one-to-one relationship in a  database schema.



2. How could you ensure that each product in the "Product" table has a valid category assigned to it?
Ans:-

// Pre-save hook to validate category before saving a product

productSchema.pre('save', async function(next) {
    const category = await Category.findById(this.category);
    if (!category) {
        throw new Error('Invalid category assigned to product');
    }
    next();
});


3. Create schema in any Database script or any ORM (Object Relational Mapping).
Ans:-

const mongoose = require('mongoose');

// Define schema for Product

const productSchema = new mongoose.Schema({
    name: { type: String, required: true },
    price: { type: Number, required: true },
    category: { type: mongoose.Schema.Types.ObjectId, ref: 'Category', required: true }
});


// Define schema for Category

const categorySchema = new mongoose.Schema({
    name: { type: String, required: true, unique: true }
});


// Create models based on defined schemas

const Product = mongoose.model('Product', productSchema);
const Category = mongoose.model('Category', categorySchema);

module.exports = { Product, Category };