# CSFML Bindings for Racket

This is a _complete_ FFI wrapper for [CSFML 2.5][csfml]. It also consists of extra, helper functions in the same style to simplify very common code (e.g. event handling).

## Quickstart Example

It's expected that you know [CSFML][csfml] and know the types, functions, etc. But, here's an example of it being used to render to a window:

```racket
(require csfml)

(define (process-events window)
  (let ([event (sfRenderWindow_pollEvent window)])
    (when event
      (case (sfEvent-type event)
        ('sfEvtKeyPressed
          (case (sfKeyEvent-code (sfEvent-key event))
            ('sfKeyEscape (sfRenderWindow_close window)))))

      ;; there may be more events to process
      (process-events window))))

(define (render window)
  (sfRenderWindow_clear window sfRed)
  (sfRenderWindow_display window))

(define (run-loop window)
  (process-events window)
  (render window)

  ;; loop forever until closed
  (when (sfRenderWindow_isOpen window)
    (run-loop window)))

;; create the window
(define mode (make-sfVideoMode 640 480 32))
(define window (sfRenderWindow_create mode "Example" '(sfDefaultStyle) #f))

;; run
(run-loop window)
```

## Initialization Fields



[csfml]: https://www.sfml-dev.org/
