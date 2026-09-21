---
layout: "@layouts/Layoutmd.astro"
title: JavaScript Structure
date: 10 Ene 2026
author: Damian Ruiz
desc: Lorem ipsum, dolor sit amet consectetur adipisicing elit. Accusantium labore quia molestiae voluptatum necessitatibus iure cumque sequi blanditiis iste quo totam cum, assumenda maiores ullam distinctio ab autem ipsam rem?
image: https://th.bing.com/th/id/OIP.VtoIcjP02Hzhkj69RvNAigHaHa?w=173&h=181&c=7&r=0&o=7&dpr=1.3&pid=1.7&rm=3
---

# JavaScript Structure

![html](https://th.bing.com/th/id/OIP.VtoIcjP02Hzhkj69RvNAigHaHa?w=173&h=181&c=7&r=0&o=7&dpr=1.3&pid=1.7&rm=3)

Lorem ipsum, dolor sit amet consectetur adipisicing elit. Accusantium labore quia molestiae voluptatum necessitatibus iure cumque sequi blanditiis iste quo totam cum, assumenda maiores ullam distinctio ab autem ipsam rem?


``` js

    /**
 * Calculate the Greatest Common Divisor (GCD) using Euclidean algorithm
 * @param {number} a 
 * @param {number} b 
 * @returns {number} GCD of a and b
 */
function gcd(a, b) {
    a = Math.abs(a);
    b = Math.abs(b);
    while (b !== 0) {
        let temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}

/**
 * Calculate the Least Common Multiple (LCM)
 * @param {number} a 
 * @param {number} b 
 * @returns {number} LCM of a and b
 */
function lcm(a, b) {
    if (a === 0 || b === 0) return 0; // LCM involving zero is zero
    return Math.abs(a * b) / gcd(a, b);
}

/**
 * Validate that the input is a finite integer
 * @param {*} value 
 * @returns {boolean}
 */
function isValidInteger(value) {
    return Number.isInteger(value) && Number.isFinite(value);
}

// Example usage:
try {
    let num1 = 12;
    let num2 = 18;

    if (!isValidInteger(num1) || !isValidInteger(num2)) {
        throw new Error("Inputs must be valid integers.");
    }

    console.log(`LCM of ${num1} and ${num2} is: ${lcm(num1, num2)}`);
} catch (error) {
    console.error("Error:", error.message);
}


```