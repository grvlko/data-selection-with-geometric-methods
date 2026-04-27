# data-selection-with-geometric-methods

Исследование направлено на валидацию методов отбора данных, основанных на геометрических свойствах внутренних представлений. Мы проверяем гипотезу о том, что геометрические метрики, такие как внутренняя размерность (Intrinsic Dimensionality, Effective Rank), позволяют идентифицировать наиболее информативные примеры эффективнее, чем стандартные эвристические или статистические методы

## Методология

В качестве базовой модели будет использоваться moded GPT. Эксперимент заключается в сравнении эффективности обучения модели на подмножествах данных, отобранных с помощью различных стратегий

Для оценки эффективности будут реализованы 4 базовых метода:
- Random Sampling
- Perplexity Filtering
- ID filtering

Сравнение будет проводиться на четырех объемах обучающей выборки для анализа масштабируемости методов: 10%, 30% 70% от общего объема данных и 100% (Обучение на полном датасете для определения верхнего предела качества).

## Результат

Кривые обучения (scaling laws), демонстрирующие остуствие преимущества геометрические методов перед baseline-подходами в `geom-distill-experiment.ipynb` на gpt-2-like модели размером 6М, датасете wikitext-2 и `geom_distill_experiment_wikitext-103.ipynb` на gpt-2-like модели размером 12М, датасете wikitext-103.

В поисках причин отсутствия результата в `diversity_of_geom.ipynb` проверяется разнообразие отфильтрованных по ID данных. С этим проблем нет, откуда мы делаем вывод, что основная проблема это маленький размер моделей, не способных эффективно обучаться на сложных данных, оставленных геометрической фильтрацией.

Дополнительно попробовали комбинацию геометрических метрик в `geom-to-utility-proxy-selection.ipynb`, результат незначительно улучшился. Проверили гипотезу в рамках CV в `resnet_cifar100_geom_distill.ipynb`, получили аналогичные неудовлетворительные результаты.

Также в `mnist_forgetting_selected_advantage.ipynb` воспроизведен один из результататов статьи arxiv.org:2306.04723, на котором основывается наша гипотеза. При обучении модели на данных, очиенных от примеров, которые модель выучивает и не забывает, метрики почти не ухудшаются. Так можно ускорить обучение на 70%.

## Статьи:

- When Less is More: Investigating Data Pruning for Pretraining LLMs at Scale
- RETHINKING DATA SELECTION AT SCALE: RANDOM SELECTION IS ALMOST ALL YOU NEED
- Intrinsic Dimension Estimation for Robust Detection of AI-Generated Texts
- From Internal Representations to Text Quality: A Geometric Approach to LLM Evaluation
- The Best of Both Worlds: Bridging Quality and Diversity in Data Selection with Bipartite Graph
- Data Diversity Matters for Robust Instruction Tuning
- An Empirical Study of Example Forgetting during Deep Neural Network Learning

## Команда

- Кононов Григорий
- Лебедев Иван
- Кулаковский Даниил

