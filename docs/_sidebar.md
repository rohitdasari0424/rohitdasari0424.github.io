<p align = "center" style = "font-size : 26px">FTC Mecanum Path Following</p>


  * Quickstart
     * [Get Started](/get-started.md)
     * [Frequently Asked Questions](/faq.md)
     * [Path-Follower Mechanics](/path-follow-mechanics.md)

  * Before You Start
    * Terms To know
      * [Odometry](/odometry-term.md)
      * [Dead Wheels](/dead-wheels-term.md)
      * [PID](/pid-term.md)
      * [Path](/path-term.md)
      * [Path Generation](/path-generation-term.md)
      * [Lookahead Point](/lookahead-point-term.md)
      * [Field Centric](/field-centric-term.md)
    * [Essential Functions](/essential-functions.md)
    * [Installations](/installation.md)

  * Hardware Classes
    * [Motor Class](/motor-class.md)
    * [Mecanum Class](/mecanum-class.md)
    * [Encoders Test](/encoder-test.md)

  * Code Implementations
    * [Overview](/code-implementation-overview.md)
    * [Point Class](/Point.md)
    * PID Controller
      * [Set Up](/pid-overview.md)
      * [P-Value](/p-value.md)
      * [Delta-Time](/delta-time.md)
      * [I-Value](/I-Value.md)
      * [D-Value](/D-Value.md)
      * [Final Result](/pid-final-result.md)
    * Odometry
      * [Set Up](/odometry-overview.md)
      * [Update Tracker](/update-tracker.md)
      * [Final Result](/odometry-final-result.md)
    * Lookahead Point
      * [Set Up](/lookahead-point-overview.md)
      * [Line Circle Intersection](/line-circle-intersection.md)
      * [Clip to Line](/clip-to-line.md)
      * [Clip to Path](/clip-to-path.md)
      * [Get Lookahead](/get-lookahead.md)
      * [Heading Point](/heading-point.md)
      * [Final Result](/lookahead-final-result.md)
    * Movement Code
      * [Overview](/movement-code-overview.md)
      * [Field Centric](/field-centric.md)
      * [Go To Position](/go-to-position.md)
      * [Follow Path](/follow-path.md)
    
* Tuning
  * [Overview](/pid-tuning-overview.md)
  * [Constants Interface](/constants-interface.md)
  * PID Controller
    * [Tuner Method](/tuner-method.md)
    * [Turn Controller](/turn-controller.md)
    * [Drive Controller](/drive-controller.md)
    * [Strafe Controller](/strafe-controller.md)
  * Odometry
    * [Track Width Tuning](/trackwidth-tuner.md)
    * [Aux Width Tuning](/aux-width-tuning.md)
* Testing
  * [Odometry](/odometry-test.md)
  * [Lookahead Test](/lookahead-test.md)
  * [PID Controllers](/go-to-point-test.md)
  * [Path Following](/path-following-test.md)
