# spt-tarkov
I have a problem with creating a mod. Help with advice please.

module.exports = function(myMod) {
    let healInterval = 10; // Интервал лечения в секундах
    let healAmount = 5; // Количество здоровья, восстанавливаемое за раз
    let lastHealTime = 0; // Время последнего лечения

    // Хук, который срабатывает каждый кадр игры
    myMod.hook('OnGameUpdate', (time) => {
        // Проверяем, прошло ли достаточно времени с последнего лечения
        if (time - lastHealTime >= healInterval) {
            const player = myMod.player; // Получаем данные игрока
            if (player && player.health) {
                // Лечим каждую часть тела
                for (const bodyPart in player.health) {
                    if (player.health[bodyPart].current < player.health[bodyPart].maximum) {
                        player.health[bodyPart].current = Math.min(
                            player.health[bodyPart].current + healAmount,
                            player.health[bodyPart].maximum
                        );
                    }
                }
                console.log(`Персонаж вылечен на ${healAmount} HP!`);
            }
            lastHealTime = time; // Обновляем время последнего лечения
        }
    });
};

Mistake in this:
Мод (my_custom_mod) несовместим, поскольку он не реализует хотя бы один из следующих методов: IPostSptLoadMod, IPostDBLoadMod, IPreSptLoadMod
