// Yaqeen's Birthday Jungle Game 🎉

import { useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Sparkles } from "lucide-react";
import { motion } from "framer-motion";

const villains = [
  "Giggly Gorilla",
  "Ticklish Tarantula",
  "Sneaky Snake",
  "Prankster Parrot",
  "Dizzy Jaguar"
];

const facts = [
  "🦜 Parrots in the Amazon can mimic human voices!",
  "🐍 The green anaconda is one of the heaviest snakes in the world!",
  "🐒 Spider monkeys swing with their tails like extra arms!",
  "🐸 Some Amazon frogs are so small they can sit on a fingernail!",
  "🦋 There are butterflies in the Amazon with transparent wings!"
];

export default function YaqeenBirthdayGame() {
  const [popped, setPopped] = useState(Array(villains.length).fill(false));
  const [showHero, setShowHero] = useState(false);

  const popVillain = (index) => {
    const newPopped = [...popped];
    newPopped[index] = true;
    setPopped(newPopped);
    if (newPopped.every((val) => val)) {
      setTimeout(() => setShowHero(true), 1000);
    }
  };

  return (
    <div className="min-h-screen bg-green-100 flex flex-col items-center p-6 space-y-6">
      <h1 className="text-4xl font-bold text-green-800">🌴 Welcome to Yaqeen's Jungle Birthday Adventure! 🌴</h1>

      <div className="grid grid-cols-2 md:grid-cols-3 gap-4">
        {villains.map((villain, index) => (
          <motion.div
            key={index}
            whileHover={{ scale: 1.05 }}
            whileTap={{ scale: 0.9 }}
          >
            <Card className="cursor-pointer bg-yellow-100 text-center shadow-lg" onClick={() => popVillain(index)}>
              <CardContent className="p-6 text-lg font-semibold">
                {popped[index] ? `💥 You popped ${villain}!` : `👀 Tap to find: ${villain}`}
              </CardContent>
            </Card>
          </motion.div>
        ))}
      </div>

      {showHero && (
        <motion.div
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          transition={{ duration: 1 }}
          className="bg-white rounded-xl p-6 mt-8 text-center max-w-2xl shadow-xl"
        >
          <h2 className="text-3xl font-bold text-blue-800">🦸‍♂️ Jungle Hero Appears!</h2>
          <p className="text-xl mt-4">Happy Birthday, <strong>Yaqeen</strong>! 🎉</p>
          <p className="text-md mt-2">The jungle is throwing a party just for you!</p>
          <div className="mt-4 space-y-2">
            {facts.map((fact, i) => (
              <motion.div key={i} initial={{ opacity: 0 }} animate={{ opacity: 1 }} transition={{ delay: i * 0.3 }}>
                {fact}
              </motion.div>
            ))}
          </div>

          <div className="mt-6">
            <pre className="text-pink-600 text-lg leading-snug">
  {`        🎂🎂🎂🎂🎂🎂🎂🎂🎂🎂🎂🎂🎂
        | H A P P Y   B I R T H D A Y |
        |         Y A Q E E N         |
        |______________________________|
       (                              )
      (   🎈🎈🎈   🎁  🎈🎈🎈   )
     (    🎉 Have a Wild Jungle Day! 🎉   )
      ------------------------------`}
            </pre>
            <Sparkles className="mx-auto mt-2 text-yellow-500 animate-ping" size={36} />
          </div>
        </motion.div>
      )}
    </div>
  );
}
