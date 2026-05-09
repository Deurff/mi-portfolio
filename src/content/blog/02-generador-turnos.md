---
title: 'Generador de turnos médicos: el proyecto que más me ha enseñado'
description: 'Un algoritmo justo para repartir guardias entre 10 médicos, con vacaciones, descansos de 48h y semilla tipo Minecraft.'
pubDate: '2026-05-09'
tags: ['medicina', 'algoritmo', 'trabajo']
heroImage: '../../assets/banner-turnos.png'
---

En mi trabajo somos 10 médicos y cada mes hay que armar el cuadro
de guardias. Suena simple hasta que cuentas las reglas.

## Las reglas que tenía que cumplir

- Descanso de 48 horas después de cada guardia
- Guardias diurnas (08:00–22:00) cubiertas por 2 médicos
- Guardias nocturnas (22:00–08:00) cubiertas por 1 médico
- Tener en cuenta la carga del mes anterior para no sobrecargar siempre a los mismos
- Recordar quién hizo la última y penúltima guardia del mes anterior, para aplicar el descanso de 48h
- Permitir marcar vacaciones por rangos de fechas
- Permitir marcar días en los que un médico prefiere no tener guardia (diurna, nocturna o ambas), siendo justo con todos
- Generación por semilla, como Minecraft, para reproducir resultados

## Cómo lo construí con Claude

[Aquí el proceso]

## Lo que aprendí

[Reflexión]