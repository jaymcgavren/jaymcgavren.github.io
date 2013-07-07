---
layout: post
title: 'Another Ruby tweet...'
tags: []
status: publish
type: post
published: true
meta:
  original_post_id: '1385'
  _wp_old_slug: '1385'
---
Was browsing the new Popular Science archives, which led to an article from 1984, which had a picture of the book <em>Creative Graphics for the BBC Microcomputer</em>, which led me to an archived copy of the book online, which had a dirt-simple program to draw Lissajous curves, which led me to write this tweetable Ruby version.  (Phew!)

<pre>ruby -rcurses -e"include Curses;i=0;loop{setpos 12*(Math.sin(i)+1),40*(Math.cos(i*0.2)+1);addstr'.';i+=0.01;refresh}" #ruby</pre>

<pre>
****         *******                ********                ******           **
*  *        **     **              **      **              **     *         * **
*  **       *       **            **        **            **       *        *  *
*   *      *         **          *           **          **        **      *   *
*   *      *          *         **             *         *          **     *   *
*    *    *            *        *              **       *            *    *    *
*    *   **             *      *                **     **            **   *    *
*    **  *              **    *                  *     *              *   *    *
*     * **               *   **                  **   *               ** *     *
*     * *                ** **                    *  *                 * *     *
*     * *                 * *                      * *                 **      *
*      **                  **                      **                   *      *
*      *                   **                       *                   *      *
*      **                 * *                      * *                 ***     *
*     * *                **  *                    *   *                * *     *
*     *  *               *   **                  **   *               ** *     *
*    *   *              *     *                  *     *              *  **    *
*    *   **            *       *                *      *             *    *    *
*   **    *            *       *               *        *            *    *    *
*   *     **          **        **            **         *          *      *   *
*   *      *         *           **           *          **         *      *   *
*  *        *       **            **        **            **       *       **  *
** *         *     **              **      **              **     **        * **
 **           ******                 *******                *******         ***
</pre>
