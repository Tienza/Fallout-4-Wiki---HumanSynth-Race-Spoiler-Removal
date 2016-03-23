// ==UserScript==
// @name         Fallout 4 Race Removal
// @namespace    http://tampermonkey.net/
// @version      2.0
// @description  Removes the "race"  bar from Human and Synth character descriptions, allowing players to read the wiki without spoiling later-game information in Fallout 4
// @author       Piradon Liengtiraphan
// @match        http://fallout.wikia.com/*
// @grant        none
// ==/UserScript==
/* jshint -W097 */
'use strict';

Element.prototype.remove = function() {
    this.parentElement.removeChild(this);
}
NodeList.prototype.remove = HTMLCollection.prototype.remove = function() {
    for(var i = this.length - 1; i >= 0; i--) {
        if(this[i] && this[i].parentElement) {
            this[i].parentElement.removeChild(this[i]);
        }
    }
}

var abcElements = document.querySelectorAll('.pi-data-value.pi-font');
for (var i = 0; i < abcElements.length; i++)
    abcElements[i].id = 'abc-' + i;

var xyzElements = document.querySelectorAll('.pi-data-label.pi-secondary-font');
for (var i = 0; i < xyzElements.length; i++)
    xyzElements[i].id = 'xyz-' + i;

if(document.getElementById('abc-0').innerHTML.includes("Fallout 4") || (document.getElementById('abc-0').innerHTML.includes("Fallout 4") && document.getElementById('abc-0').innerHTML.includes("Fallout 3"))){

    if(document.getElementById('xyz-0').innerHTML = "race" && (document.getElementById('abc-2').innerHTML.includes("Human") || document.getElementById('abc-2').innerHTML.includes("Synth"))) {
        document.getElementById('xyz-0').remove();
        document.getElementById('abc-2').remove();     
    } 

    else
        document.getElementById('xyz-0').innerHTML = "race";
}