# recetas-app
recetas 
import React, { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Input } from "@/components/ui/input";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";
import { Share2 } from "lucide-react";

const recipes = [
  {
    title: "Spaghetti Carbonara",
    type: "Plato Principal",
    image: "https://source.unsplash.com/featured/?spaghetti",
    description: "Clásica receta italiana con panceta, huevos y parmesano."
  },
  {
    title: "Tacos al Pastor",
    type: "Plato Principal",
    image: "https://source.unsplash.com/featured/?tacos",
    description: "Deliciosos tacos con carne marinada al estilo mexicano."
  },
  {
    title: "Paella Valenciana",
    type: "Plato Principal",
    image: "https://source.unsplash.com/featured/?paella",
    description: "Arroz con mariscos, pollo y verduras, un plato español icónico."
  },
  {
    title: "Sushi Variado",
    type: "Plato Principal",
    image: "https://source.unsplash.com/featured/?sushi",
    description: "Rolls de arroz, pescado y vegetales frescos."
  },
  {
    title: "Brownies de Chocolate",
    type: "Postre",
    image: "https://source.unsplash.com/featured/?brownie",
    description: "Postre húmedo, denso y con intenso sabor a chocolate."
  },
  {
    title: "Flan Casero",
    type: "Postre",
    image: "https://source.unsplash.com/featured/?flan",
    description: "Delicioso flan de huevo con caramelo."
  },
  {
    title: "Pollo al Curry",
    type: "Plato Principal",
    image: "https://source.unsplash.com/featured/?curry",
    description: "Receta asiática con especias y leche de coco."
  },
  {
    title: "Pizza Margarita",
    type: "Plato Principal",
    image: "https://source.unsplash.com/featured/?pizza",
    description: "Clásica pizza italiana con tomate, mozzarella y albahaca."
  },
  {
    title: "Ceviche Peruano",
    type: "Entrada",
    image: "https://source.unsplash.com/featured/?ceviche",
    description: "Pescado marinado en limón con cebolla y ají."
  },
  {
    title: "Churros con Chocolate",
    type: "Postre",
    image: "https://source.unsplash.com/featured/?churros",
    description: "Tradicional dulce español servido con chocolate caliente."
  },
];

export default function RecetasPage() {
  const [search, setSearch] = useState("");
  const [filter, setFilter] = useState("Todos");

  const filteredRecipes = recipes.filter((r) => {
    const matchesSearch = r.title.toLowerCase().includes(search.toLowerCase());
    const matchesFilter = filter === "Todos" || r.type === filter;
    return matchesSearch && matchesFilter;
  });

  const shareRecipe = (title) => {
    const url = window.location.href;
    navigator.clipboard.writeText(`${title} - ${url}`);
    alert("¡Receta copiada para compartir!");
  };

  const recipeTypes = ["Todos", "Plato Principal", "Postre", "Entrada"];

  return (
    <div className="p-6 max-w-screen-xl mx-auto bg-gradient-to-tr from-yellow-50 via-rose-50 to-orange-100 min-h-screen">
      <h1 className="text-5xl font-extrabold text-center mb-6 text-orange-600 drop-shadow-sm">Recetario Internacional</h1>
      <div className="flex flex-col md:flex-row items-center gap-4 mb-6">
        <Input
          placeholder="Buscar receta..."
          value={search}
          onChange={(e) => setSearch(e.target.value)}
          className="w-full md:w-1/2 border-orange-300 focus:ring-orange-500"
        />
        <select
          className="border rounded-md p-2 border-orange-300 text-orange-700 bg-orange-50"
          value={filter}
          onChange={(e) => setFilter(e.target.value)}
        >
          {recipeTypes.map((type) => (
            <option key={type} value={type}>{type}</option>
          ))}
        </select>
      </div>
      <div className="grid gap-6 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4">
        {filteredRecipes.map((recipe, idx) => (
          <motion.div
            key={idx}
            whileHover={{ scale: 1.03 }}
            className="transition duration-200"
          >
            <Card className="rounded-2xl shadow-xl overflow-hidden bg-white border border-orange-100">
              <img
                src={recipe.image}
                alt={recipe.title}
                className="h-40 w-full object-cover"
              />
              <CardContent className="p-4">
                <h2 className="text-xl font-bold mb-1 text-orange-700">{recipe.title}</h2>
                <p className="text-sm text-gray-600 mb-2">{recipe.description}</p>
                <Button
                  variant="outline"
                  size="sm"
                  onClick={() => shareRecipe(recipe.title)}
                  className="flex items-center gap-2 text-sm border-orange-300 text-orange-700 hover:bg-orange-50"
                >
                  <Share2 className="w-4 h-4" /> Compartir
                </Button>
              </CardContent>
            </Card>
          </motion.div>
        ))}
      </div>
    </div>
  );
}
